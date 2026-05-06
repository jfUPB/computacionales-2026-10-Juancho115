NO PRESENTÓ LA UNIDAD y tampoco la sustentación


# Unidad 7

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### 1

`triangle.cpp`

```cpp
#include <iostream>
#include <cmath>
#include <glad/glad.h>
#include <GLFW/glfw3.h>


// Callback: ajusta el viewport cuando cambie el tamaño de la ventana
void framebuffer_size_callback(GLFWwindow* window, int width, int height) {
	glViewport(0, 0, width, height);
}

// Procesa entrada simple: cierra con ESC
void processInput(GLFWwindow* window) {
	if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
		glfwSetWindowShouldClose(window, true);
}

// Tamaño de las ventanas
const unsigned int SCR_WIDTH = 400;
const unsigned int SCR_HEIGHT = 400;

// Fuentes de los shaders
const char* vertexShaderSrc = R"glsl(
	#version 460 core
	layout(location = 0) in vec3 aPos;
	uniform vec2 offset;
	void main() {
		vec3 newPos = aPos;
		newPos.xy += offset;
		gl_Position = vec4(newPos, 1.0);
	}
)glsl";

const char* fragmentShaderSrc = R"glsl(
	#version 460 core
	out vec4 FragColor;
	uniform vec4 ourColor;
	void main() {
		FragColor = ourColor;
	}
)glsl";

// IDs globales
unsigned int VAO, VBO;
unsigned int shaderProg;

// Compila y linkea un programa de shaders, retorna su ID
unsigned int buildShaderProgram() {
	int success;
	char log[512];

	unsigned int vs = glCreateShader(GL_VERTEX_SHADER);
	glShaderSource(vs, 1, &vertexShaderSrc, nullptr);
	glCompileShader(vs);
	glGetShaderiv(vs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(vs, 512, nullptr, log);
		std::cerr << "ERROR VERTEX SHADER:\n" << log << "\n";
	}

	unsigned int fs = glCreateShader(GL_FRAGMENT_SHADER);
	glShaderSource(fs, 1, &fragmentShaderSrc, nullptr);
	glCompileShader(fs);
	glGetShaderiv(fs, GL_COMPILE_STATUS, &success);
	if (!success) {
		glGetShaderInfoLog(fs, 512, nullptr, log);
		std::cerr << "ERROR FRAGMENT SHADER:\n" << log << "\n";
	}

	unsigned int prog = glCreateProgram();
	glAttachShader(prog, vs);
	glAttachShader(prog, fs);
	glLinkProgram(prog);
	glGetProgramiv(prog, GL_LINK_STATUS, &success);
	if (!success) {
		glGetProgramInfoLog(prog, 512, nullptr, log);
		std::cerr << "ERROR LINKING PROGRAM:\n" << log << "\n";
	}

	glDeleteShader(vs);
	glDeleteShader(fs);
	return prog;
}

// Crea un VAO/VBO con los datos de un triángulo
void setupTriangle() {
	float vertices[] = {
		-0.5f, -0.5f, 0.0f,
		 0.5f, -0.5f, 0.0f,
		 0.0f,  0.5f, 0.0f
	};
	glGenVertexArrays(1, &VAO);
	glGenBuffers(1, &VBO);

	glBindVertexArray(VAO);
	glBindBuffer(GL_ARRAY_BUFFER, VBO);
	glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
	glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 3 * sizeof(float), (void*)0);
	glEnableVertexAttribArray(0);
	glBindVertexArray(0);
}


int main()
{
	// 1) Inicializar GLFW
	if (!glfwInit()) {
		std::cerr << "Fallo al inicializar GLFW\n";
		return -1;
	}
	glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 4);
	glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 6);
	glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

	// 2) Crear ventana
	GLFWwindow* mainWindow = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Ventana", nullptr, nullptr);
	if (!mainWindow) {
		std::cerr << "Error creando ventana1\n";
		glfwTerminate();
		return -1;
	}

	// 3) Lee el tamaño del framebuffer
	int bufferWidth, bufferHeight;
	glfwGetFramebufferSize(mainWindow, &bufferWidth, &bufferHeight);
	
	// 4) Callbacks 
	glfwSetFramebufferSizeCallback(mainWindow, framebuffer_size_callback);


	// 5) Cargar GLAD y recursos en contexto de window1
	glfwMakeContextCurrent(mainWindow);

	if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress)) {
		std::cerr << "Fallo al cargar GLAD (contexto1)\n";
		return -1;
	}

	// 6) Habilita el V-Sync
	glfwSwapInterval(1);

	// 7) Compila y linkea shaders
	shaderProg = buildShaderProgram();
	glUseProgram(shaderProg);
	int offsetLocation = glGetUniformLocation(shaderProg, "offset");
	int colorLocation = glGetUniformLocation(shaderProg, "ourColor");

	// 8) Genera el contenido a mostrar
	setupTriangle();

	// 9) Configura el viewport
	glViewport(0, 0, bufferWidth, bufferHeight);


	// 10) Loop principal
	while (!glfwWindowShouldClose(mainWindow))
	{
		// 11) Manejo de eventos
		glfwPollEvents();

	
		// 12) Procesa la entrada
		processInput(mainWindow);

		// 13) Configura el color de fondo y limpia el framebuffer
		glClearColor(0.2f, 0.3f, 0.3f, 1.0f);
		glClear(GL_COLOR_BUFFER_BIT);
		
        // 14) Indica a OpenGL que use el shader program
		glUseProgram(shaderProg);

		int currentWidth, currentHeight;
		glfwGetFramebufferSize(mainWindow, &currentWidth, &currentHeight);

		double xpos, ypos;
		glfwGetCursorPos(mainWindow, &xpos, &ypos);

		float x = currentWidth > 0 ? static_cast<float>(xpos) / currentWidth : 0.0f;
		float y = currentHeight > 0 ? static_cast<float>(ypos) / currentHeight : 0.0f;
		if (x < 0.0f) x = 0.0f;
		if (x > 1.0f) x = 1.0f;
		if (y < 0.0f) y = 0.0f;
		if (y > 1.0f) y = 1.0f;

		float timeValue = static_cast<float>(glfwGetTime());
		float red = std::sin(timeValue) * 0.5f + 0.5f;
		glUniform4f(colorLocation, red, x, y, 1.0f);
		glUniform2f(offsetLocation, x * 2.0f - 1.0f, 1.0f - y * 2.0f);

		// 15) Activa el VAO y dibuja el triángulo
		glBindVertexArray(VAO);
		glDrawArrays(GL_TRIANGLES, 0, 3);

		// 16) Intercambia buffers y muestra el contenido
		glfwSwapBuffers(mainWindow);
	}

	// 17) Limpieza
	glfwMakeContextCurrent(mainWindow);
	glDeleteVertexArrays(1, &VAO);
	glDeleteBuffers(1, &VBO);
	glDeleteProgram(shaderProg);

	glfwDestroyWindow(mainWindow);
	glfwTerminate();
	return 0;
}
```

### 2
#### Contexto y carga de OpenGL

<img width="511" height="122" alt="image" src="https://github.com/user-attachments/assets/358dd0d7-6dc6-41a8-a15d-602a9729de92" />

<img width="865" height="122" alt="image" src="https://github.com/user-attachments/assets/d0291b5d-c14b-4c6d-9cab-f5a0ecc1d7a6" />

<img width="609" height="44" alt="image" src="https://github.com/user-attachments/assets/4de5bf60-b104-4b23-8764-12b90519e6df" />

<img width="688" height="80" alt="image" src="https://github.com/user-attachments/assets/5e99e7f6-ec12-4613-bb23-1d0806fc518d" />

Primero inicializo GLFW porque es la librería que crea la ventana y el contexto OpenGL. Sin contexto activo, GLAD no puede cargar las funciones modernas. Por eso gladLoadGLLoader va después de glfwMakeContextCurrent. Si se invierte el orden, las direcciones de funciones son nulas y OpenGL falla.


#### Del arreglo al shader

<img width="987" height="662" alt="image" src="https://github.com/user-attachments/assets/aa0ec02a-33fa-4312-9f2d-957d9bb4524d" />

<img width="884" height="628" alt="image" src="https://github.com/user-attachments/assets/5f03252f-be6c-48b1-b3a7-c9313f390f40" />

El arreglo vertices[] se envía al VBO con glBufferData. Luego el VAO guarda la configuración con glVertexAttribPointer(0, 3, ...).
En el shader, layout(location = 0) in vec3 aPos recibe ese atributo. Así el arreglo termina alimentando el vertex shader.

#### Uniform y cambio visual

<img width="889" height="505" alt="image" src="https://github.com/user-attachments/assets/8e5773d1-496b-4801-a7ef-2a08e14c7c32" />

<img width="879" height="462" alt="image" src="https://github.com/user-attachments/assets/439e543b-003b-4816-9d08-2f8952d749f4" />

El color y el offset cambian cada frame usando uniforms. El VBO no se modifica (no hay glBufferData en el loop).
Esto es posible porque un uniform actualiza valores globales del shader en cada draw call sin tocar los datos de vértices.

#### Prueba de borde

<img width="425" height="459" alt="image" src="https://github.com/user-attachments/assets/1d388574-7892-4d3f-897d-81a04d8d989f" />

Esperaba que el triángulo saliera del rango visible (NDC). Al usar offset (2,2), el triángulo desaparece o queda fuera. Concluyo que el problema visual proviene del estado/uniform y no del VBO, porque los datos de vértice no cambiaron.

#### Responsabilidad del pipeline

<img width="469" height="327" alt="image" src="https://github.com/user-attachments/assets/ea61118b-1b1d-4d18-afd3-33659c1267c9" />

<img width="678" height="53" alt="image" src="https://github.com/user-attachments/assets/1dccb87f-5542-428e-95ae-7e84e08ed2bc" />

Uso uniform porque el color y la posición cambian por frame, no por vértice. Si fueran atributos, tendría que duplicar datos en el VBO. Esto separa responsabilidades: VBO = geometría, uniforms = control dinámico.

## Bitácora de reflexión
