El proyecto fue hacer un agente que juega Buscaminas usando Aprendizaje por Refuerzo. La idea principal es que el agente no sabe dónde están las minas al inicio — aprende solo jugando partidas una y otra vez.
El entorno
Se armó un tablero de 3x3 con 2 minas. El tablero tiene dos capas: la real (donde están las minas y los números) que el agente nunca ve directamente, y la visible que es lo que el agente percibe — casillas cerradas, abiertas con número, o minas pisadas.
El agente
Usa UCB como estrategia de decisión. La gracia de UCB es que no explora al azar como haría epsilon-greedy — es más inteligente. Tiene una fórmula que balancea dos cosas: qué tan buena fue una casilla en el pasado (explotación) y qué tan poco la ha visitado (exploración). Con el tiempo, conforme va conociendo el tablero, explora menos y explota más, de forma automática.
El aprendizaje
Cada vez que el agente abre una casilla recibe una recompensa: +1 si es segura, -5 si es mina, +3 si gana. Esa recompensa actualiza una tabla Q que guarda cuánto vale cada casilla según la experiencia acumulada. Con 500 partidas el agente ya tiene bastante experiencia guardada.
La mejora al pasar a 3x3
El tablero original era 4x4 con 3 minas. Al bajarlo a 3x3 con 2 minas el agente mejoró bastante porque hay menos casillas posibles, entonces aprende más rápido y la tabla Q se llena con experiencia más relevante en menos episodios.
