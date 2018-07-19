# Información general

## [¿Qué es SQL Server Machine Learning Services?](what-is-sql-server-machine-learning.md)
### [Análisis en base de datos](r/sql-server-r-services.md)
### [Servidor independiente](r/r-server-standalone.md)
## [Nuevas características](what-s-new-in-sql-server-machine-learning-services.md)
## [Características por edición](r/differences-in-r-features-between-editions-of-sql-server.md)

# [Arquitectura](architecture-overview-machine-learning.md)
## [R](r/architecture-overview-sql-server-r.md)
### [Interoperabilidad de R](r/r-interoperability-in-sql-server.md)
### [Componentes que admiten la integración de R](r/new-components-in-sql-server-to-support-r.md)
### [Seguridad para R](r/security-overview-sql-server-r.md)
## [Python](python/architecture-overview-sql-server-python.md)
### [Python en Machine Learning Services](python/sql-server-python-services.md)
### [Interoperabilidad de Python](python/python-interoperability.md)
### [Componentes para admitir Python](python/new-components-in-sql-server-to-support-python-integration.md)
### [Seguridad de Python](python/security-overview-sql-server-python-services.md)
<!-- ### [How To Create a Resource Pool for Python](python/how-to-create-a-resource-pool-for-python.md)-->
<!-- ### [Extended Events for Python](python/extended-events-for-python.md)-->
<!-- ### [DMVs for Python](python/dmvs-for-python.md)-->
<!-- ### [Resource Governance for Python](python/resource-governance-for-python.md)-->

# Install 

## SQL Server 2017
### [Análisis en base de datos](install/sql-machine-learning-services-windows-install.md)
### [Servidor independiente](install/sql-machine-learning-standalone-windows-install.md)
## SQL Server 2016
### [R Services (en bases de datos)](install/sql-r-services-windows-install.md)
### [R Server (Standalone)](install/sql-r-standalone-windows-install.md)
## [Modelos entrenados previamente](r/install-pretrained-models-sql-server.md)
## [Instalación del símbolo del sistema](install/sql-ml-component-commandline-install.md)
## [Instalación sin conexión (sin Internet)](install/sql-ml-component-install-without-internet-access.md)
## [Actualización R y Python](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
## [Configuración de las herramientas de R](r/set-up-a-data-science-client.md)
## [Configuración de las herramientas de Python](python/setup-python-client-tools-sql.md)

# Tutoriales rápidos

## R
### [Hola mundo en R y SQL](tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
### [Control de entradas y salidas](tutorials/rtsql-working-with-inputs-and-outputs.md)
### [Control de tipos de datos y objetos](tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)
### [Crear un modelo predictivo](tutorials/rtsql-create-a-predictive-model-r.md)
### [Predecir y trazar a partir del modelo](tutorials/rtsql-predict-and-plot-from-model.md)

# [Tutoriales](tutorials/machine-learning-services-tutorials.md)
## [R](tutorials/sql-server-r-tutorials.md)
### [Información sobre análisis en base de datos](tutorials/sqldev-in-database-r-for-sql-developers.md)
#### [1. Obtener datos y scripts](tutorials/sqldev-download-the-sample-data.md)
#### [2. Configurar el entorno](r/sqldev-import-data-to-sql-server-using-powershell.md)
#### [3. Visualizar los datos](tutorials/sqldev-explore-and-visualize-the-data.md)
#### [4. Crear características de datos](tutorials/sqldev-create-data-features-using-t-sql.md)
#### [5.-Entrenar y guardar en SQL](r/sqldev-train-and-save-a-model-using-t-sql.md)
#### [6. Predecir los resultados](tutorials/sqldev-operationalize-the-model.md)

### [Tutorial integral de ciencia de datos](tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
#### [Preparar datos](tutorials/walkthrough-prepare-the-data.md)
#### [Explorar datos con SQL](tutorials/walkthrough-view-and-explore-the-data.md)
#### [Resumir datos con R](tutorials/walkthrough-view-and-summarize-data-using-r.md)
#### [Crear gráficos y trazados](tutorials/walkthrough-create-graphs-and-plots-using-r.md)
#### [Crear características de datos](tutorials/walkthrough-create-data-features.md)
#### [Generar y guardar el modelo](tutorials/walkthrough-build-and-save-the-model.md)
#### [Implementar y usar el modelo](tutorials/walkthrough-deploy-and-use-the-model.md)

### [Profundizar con RevoScaleR](tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
#### [Crear bases de datos y permisos](tutorials/deepdive-work-with-sql-server-data-using-r.md)
#### [Crear objetos de datos mediante RxSqlServerData](tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
#### [Consultar y modificar datos](tutorials/deepdive-query-and-modify-the-sql-server-data.md)
#### [Definir un contexto de cálculo](tutorials/deepdive-define-and-use-compute-contexts.md)
#### [Crear y ejecutar scripts de R](tutorials/deepdive-create-and-run-r-scripts.md)
#### [Visualizar datos](tutorials/deepdive-visualize-sql-server-data-using-r.md)
#### [Crear modelos](tutorials/deepdive-create-models.md)
#### [Puntuación de nuevos datos](tutorials/deepdive-score-new-data.md)
#### [Transformar datos](tutorials/deepdive-transform-data-using-r.md)
#### [Cargar datos en memoria mediante rxImport](tutorials/deepdive-load-data-into-memory-using-rximport.md)
#### [Crear una tabla mediante rxDataStep](tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
#### [Realizar análisis de fragmentación mediante rxDataStep](tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
#### [Analizar datos en el contexto del proceso local](tutorials/deepdive-analyze-data-in-local-compute-context.md)
#### [Mover datos entre SQL Server y el archivo XDF](tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
#### [Crear una simulación sencilla](tutorials/deepdive-create-a-simple-simulation.md)

## [Python](tutorials/sql-server-python-tutorials.md)
### [Ejecutar Python mediante T-SQL](tutorials/run-python-using-t-sql.md)
#### [Encapsulamiento de Python en un procedimiento almacenado](tutorials/wrap-python-in-tsql-stored-procedure.md)
#### [Entrenamiento y puntuación de un modelo de Python en SQL Server](tutorials/train-score-using-python-in-tsql.md)
#### [Creación de un modelo usando revoscalepy en un contexto de proceso de SQL Server](tutorials/use-python-revoscalepy-to-create-model.md)
### [Información sobre análisis en base de datos](tutorials/sqldev-in-database-python-for-sql-developers.md)
#### [Obtener datos y scripts](tutorials/sqldev-py1-download-the-sample-data.md)
#### [Importar datos](tutorials/sqldev-py2-import-data-to-sql-server-using-powershell.md)
#### [Explorar y visualizar datos](tutorials/sqldev-py3-explore-and-visualize-the-data.md)
#### [Crear características de datos](tutorials/sqldev-py4-create-data-features-using-t-sql.md)
#### [Entrenar y guardar el modelo](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)
#### [Hacer operativo el modelo](tutorials/sqldev-py6-operationalize-the-model.md)

# [Ejemplos](https://github.com/Microsoft/sql-server-samples)

# [Soluciones](tutorials/data-science-scenarios-and-solution-templates.md)

# [Procedimiento](r/sql-server-machine-learning-tasks.md)

## Administración de paquetes
### [Paquetes predeterminados](r/installing-and-managing-r-packages.md)
### [Obtención de información del paquete](r/determine-which-packages-are-installed-on-sql-server.md)
### [Instalación de paquetes de Python adicionales](python/install-additional-python-packages-on-sql-server.md)
### [Instalación de paquetes de R adicionales](r/install-additional-r-packages-on-sql-server.md)
#### [Uso de administradores de paquetes de R](r/use-r-package-managers-on-sql-server.md)
#### [Uso de T-SQL](r/install-r-packages-tsql.md)
#### [Uso de RevoScaleR](r/use-revoscaler-to-manage-r-packages.md)
##### [Habilitación de la administración de paquetes de R remota](r/r-package-how-to-enable-or-disable.md)
##### [Sincronización de paquetes de R](r/package-install-uninstall-and-sync.md)
#### [Creación de un repositorio de miniCRAN](r/create-a-local-package-repository-using-minicran.md)
#### [Sugerencias para usar paquetes de R](r/packages-installed-in-user-libraries.md)

## Modelado y exploración de datos
### [Bibliotecas de R y tipos de datos](r/r-libraries-and-data-types.md)
### [Bibliotecas de Python y tipos de datos](python/python-libraries-and-data-types.md)
### [Puntuación nativa](sql-native-scoring.md)
### [Puntuación en tiempo real](real-time-scoring.md)
### [Modelado de predicción con R](r/data-exploration-and-predictive-modeling-with-r.md)
### [Cómo efectuar una puntuación nativa o en tiempo real](r/how-to-do-realtime-scoring.md)
### [Cargar objetos de R mediante ODBC](r/save-and-load-r-objects-from-sql-server-using-odbc.md)
### [Convertir el código de R para usarlo en Machine Learning Services](r/converting-r-code-for-use-in-sql-server.md)
### [Crear varios modelos mediante rxExecBy](r/creating-multiple-models-using-rxexecby.md)
### [Usar datos de cubos OLAP en R](r/using-data-from-olap-cubes-in-r.md)
### [Crear un procedimiento almacenado mediante sqlrutils](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## Rendimiento
### [Optimización del rendimiento de R: Información general](r/sql-server-r-services-performance-tuning.md)
### [Optimización del rendimiento de R: Configuración de SQL Server](r/sql-server-configuration-r-services.md)
### [Optimización del rendimiento de R: R y optimización de datos](r/r-and-data-optimization-r-services.md)
### [Optimización del rendimiento de R: Resultados](r/performance-case-study-r-services.md)
### [Usar las funciones de generación de perfiles de código de R](r/using-r-code-profiling-functions.md)

## Administración
### [Configurar y administrar R](r/configuration-sql-server-r-services.md)
### [Opciones de configuración avanzada de Machine Learning Services](r/configure-and-manage-advanced-analytics-extensions.md)
### [Consideraciones de seguridad para el tiempo de ejecución de R en SQL Server](r/security-considerations-for-the-r-runtime-in-sql-server.md)
### [Modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](r/modify-the-user-account-pool-for-sql-server-r-services.md)
### [Agregar SQLRUserGroup como usuario de base de datos](r/add-sqlrusergroup-to-database.md)
### [Implementar y usar modelos mediante servicios web](operationalization-with-mrsdeploy.md)
### [Administración y supervisión de soluciones](r/managing-and-monitoring-r-solutions.md)
### [Regulación de recursos para Machine Learning Services](r/resource-governance-for-r-services.md)
### [Creación de grupos de recursos para el aprendizaje automático](r/how-to-create-a-resource-pool-for-r.md)
### [Eventos extendidos de Machine Learning Services](r/extended-events-for-sql-server-r-services.md)
### [Eventos extendidos para la supervisión de instrucciones PREDICT](xe-event-predict-tsql.md)
### [DMV de Machine Learning Services](r/dmvs-for-sql-server-r-services.md)
### [Uso de funciones de generación de perfiles de código de R](r/using-r-code-profiling-functions.md)
### [Supervisar Machine Learning Services con informes personalizados en Management Studio](r/monitor-r-services-using-custom-reports-in-management-studio.md)

# [Referencia de paquete](r/machine-learning-services-r-reference.md)

## [MicrosoftML en SQL](using-the-microsoftml-package.md)
## [RevoScaleR en SQL](r/revoscaler-overview.md)
## [Lista de funciones de RevoScaleR para los datos de SQL Server](r/scaler-functions-for-working-with-sql-server-data.md)
## [sqlrutils en SQL](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
## [olapR en SQL](r/how-to-create-mdx-queries-using-olapr.md)
## [revoscalepy en SQL](python/what-is-revoscalepy.md)

# Recursos

## [Problemas conocidos](known-issues-for-sql-server-machine-learning-services.md)
## [Notas de la versión](https://docs.microsoft.com/sql/sql-server/sql-server-2017-release-notes)
## [Configurar una máquina virtual](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)
## [Solucionar problemas](machine-learning-troubleshooting-faq.md)
### [Recopilación de datos](data-collection-ml-troubleshooting-process.md)
### [Errores de instalación y actualización](r/upgrade-and-installation-faq-sql-server-r-services.md)
### [LaunchPad y errores de ejecución de script externos](common-issues-external-script-execution.md)
### [Errores de scripting de R](r-script-execution-errors.md)

## Blogs
### [SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/)
### [R Server](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/)
### [Aprendizaje automático](https://blogs.technet.microsoft.com/machinelearning/)

## Foros
### [SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver)
### [Machine Learning Server](https://social.msdn.microsoft.com/Forums/home?forum=MicrosoftR)
