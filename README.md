# ViajesHorizonte-App

Proyecto Intermodular 1º DAM: Sistema de Gestión de Agencia de Viajes (ViajesHorizonte-App) 

 

INTRODUCCIÓN 

 

Propósito del sistema: Aplicación de escritorio multiplataforma diseñada para centralizar la operativa de una agencia de viajes, permitiendo gestionar el catálogo de destinos turísticos, registrar clientes, tramitar reservas de paquetes y emitir comprobantes de viaje. 

Público objetivo: Agentes de viajes (creación y cobro de reservas) y administradores de la agencia (gestión de catálogo de destinos, cupos de plazas y reportes). 

Alcance formativo: Integra el diseño de base de datos relacional, la lógica de negocio orientada a objetos en Java, el control de versiones con Git y la generación/exportación de resúmenes en formatos estructurados.  

 

REQUISITOS DEL SISTEMA 

 

Requisitos Funcionales (Casos de uso clave): 

Gestión de Clientes (CRUD): Registro con validación de DNI/NIE, teléfono y correo electrónico. 

Catálogo de Destinos y Paquetes: Consulta de destinos filtrados por país, tipo de viaje (cultural, aventura, playa) y temporada. 

Motor de Reservas: Asignación de clientes a destinos con control dinámico de plazas disponibles y cálculo de importe total (precio base + suplementos + IVA). 

Emisión de Billetes/Comprobantes: Exportación del resumen de la reserva en formato estructurado (HTML o texto). 

Requisitos Técnicos y Software: 

Entorno de ejecución: Java Development Kit (JDK 17 o 21 LTS). 

Persistencia: MySQL Server 8.0 o MariaDB con conector oficial JDBC. 

Entorno de trabajo: VSCodium / Eclipse / IntelliJ IDEA y Git para control de versiones en GitHub.  

Requisitos Mínimos de Hardware: 

CPU compatible x86-64. 

4 GB de memoria RAM. 

400 MB de almacenamiento para código, dependencias y datos de prueba. 

 

INSTALACIÓN 

 

Clonar el repositorio: 

Bash 

git clone https://github.com/beatrizOO/ViajesHorizonte-App.git 
cd ViajesHorizonte-App 
 

Inicializar la base de datos (MySQL/MariaDB): 

SQL 

CREATE DATABASE IF NOT EXISTS agencia_viajes; 
USE agencia_viajes; 
 
CREATE TABLE cliente ( 
    id_cliente INT AUTO_INCREMENT PRIMARY KEY, 
    dni VARCHAR(9) UNIQUE NOT NULL, 
    nombre VARCHAR(50) NOT NULL, 
    apellidos VARCHAR(100) NOT NULL, 
    email VARCHAR(100) NOT NULL 
); 
 
CREATE TABLE destino ( 
    id_destino INT AUTO_INCREMENT PRIMARY KEY, 
    ciudad VARCHAR(50) NOT NULL, 
    pais VARCHAR(50) NOT NULL, 
    precio_base DECIMAL(10,2) NOT NULL, 
    plazas_max INT NOT NULL 
); 
 
CREATE TABLE reserva ( 
    id_reserva INT AUTO_INCREMENT PRIMARY KEY, 
    id_cliente INT NOT NULL, 
    id_destino INT NOT NULL, 
    fecha_reserva DATE NOT NULL, 
    num_plazas INT NOT NULL, 
    precio_total DECIMAL(10,2) NOT NULL, 
    FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente), 
    FOREIGN KEY (id_destino) REFERENCES destino(id_destino) 
); 
 

Compilar y ejecutar el proyecto: 

Bash 

# Compilar los paquetes del modelo, acceso a datos y vistas 
javac -d bin src/**/*.java 
 
# Ejecutar la aplicación principal 
java -cp bin com.agencia.Main 

 

USO 
 

Acceso y Menú Principal: La aplicación arranca con un menú interactivo por consola o ventana modular: 

[1] Catálogo de Destinos (Listar destinos y consultar plazas libres). 

[2] Gestión de Clientes (Alta de nuevos viajeros y consulta de historial). 

[3] Nueva Reserva (Selección guiada: Cliente -> Destino -> Número de plazas -> Confirmación y cobro). 

[4] Consultar / Cancelar Reserva (Liberación automática de las plazas devueltas). 

[5] Generar Resumen de Reserva (Exportación del itinerario y datos fiscales). 

Flujo de reserva paso a paso: 

El agente introduce el DNI del cliente; si no existe, el sistema solicita sus datos básicos para crearlo en el momento. 

Se muestra la lista de viajes con disponibilidad real (plazas_max - plazas_reservadas > 0). 

Al confirmar las plazas deseadas, el sistema verifica que no se sobrepase el cupo, calcula el importe y almacena la transacción en la base de datos. 

 

LICENCIA 

 

Tipo: MIT License. 

Términos: Permite el uso académico, modificación del código fuente y distribución libre del proyecto, exigiendo únicamente mantener los créditos de autoría originales. 

 

 