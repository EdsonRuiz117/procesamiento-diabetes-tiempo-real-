# Procesamiento en Tiempo Real con Kafka y Spark - Dataset de Diabetes

Este proyecto implementa un sistema de procesamiento en tiempo real utilizando Apache Kafka y Apache Spark para analizar datos del dataset de diabetes. El flujo consiste en simular datos en tiempo real mediante un productor Kafka y procesarlos con Spark Streaming.

## Tecnologías utilizadas

- Apache Kafka
- Apache Spark (con PySpark)
- Python 3
- kafka-python
- Máquina virtual con Ubuntu
- PuTTY (acceso remoto)

## Estructura del proyecto

- `diabetes_producer.py`: Envía datos del archivo CSV a un topic de Kafka.
- `spark_diabetes_streaming.py`: Código de Spark Streaming que lee del topic y realiza el procesamiento.
- `diabetes.csv`: Dataset utilizado para la simulación.
- `README.md`: Instrucciones del proyecto.

## Pasos realizados en PuTTY

1. **Inicio de Zookeeper**  
   ```bash
   /opt/Kafka/bin/zookeeper-server-start.sh /opt/Kafka/config/zookeeper.properties
   ```

2. **Inicio del servidor Kafka**  
   En una nueva ventana:
   ```bash
   /opt/Kafka/bin/kafka-server-start.sh /opt/Kafka/config/server.properties
   ```

3. **Creación del topic de Kafka**
   ```bash
   /opt/Kafka/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic diabetes_stream
   ```

4. **Verificación de topics creados**
   ```bash
   /opt/Kafka/bin/kafka-topics.sh --list --bootstrap-server localhost:9092
   ```

5. **Ejecución del productor (diabetes_producer.py)**
   Asegúrate de tener el archivo `diabetes.csv` en la ruta correcta:
   ```bash
   python3 diabetes_producer.py
   ```

6. **Ejecución del consumidor Spark Streaming**
   En otro terminal:
   ```bash
   spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.3 spark_diabetes_streaming.py
   ```

## Lógica del procesamiento

- El productor Kafka lee fila por fila del archivo CSV y las envía al topic `diabetes_stream`.
- Spark Streaming se conecta al topic, interpreta los datos como JSON y aplica un esquema estructurado.
- Los datos se muestran en tiempo real por consola, pudiendo realizar filtrados como pacientes con glucosa > 140, etc.

## Ejecución paso a paso

1. Clona el repositorio
2. Asegúrate de tener Spark y Kafka correctamente configurados
3. Coloca el archivo `diabetes.csv` en la carpeta del proyecto
4. Ejecuta los scripts en el orden descrito arriba
5. Observa los resultados por consola

## Autor

Nombre: Edson Andres Ruiz Linares
Curso: Big Data
Institución: Universidad Abierta y a Distancia
Fecha: Abril de 2025