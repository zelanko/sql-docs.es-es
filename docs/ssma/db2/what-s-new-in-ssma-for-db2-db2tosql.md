---
title: Novedades de SSMA para DB2 (DB2ToSQL) Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1cc38f85-3caa-42d0-8c76-a380c1d15c67
ms.author: jtoland;alexiva
ms.openlocfilehash: 53a159627750a5ec66b5aa0b3fd6510c647e26a5
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625521"
---
# <a name="whats-new-in-ssma-for-db2-db2tosql"></a>Novedades de SSMA para DB2 (DB2ToSQL)

En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para DB2 en cada versión.

## <a name="ssma-v88"></a>SSMA v8.8

La versión v8.8 de SSMA para DB2 incluye:

* Mejoras en la estabilidad de sincronización de objetos de SQL Server
* Mejoras en el rendimiento de la interfaz gráfica de usuario durante la evaluación y la conversión
* Se ha `ROWID` `varbinary(40)` actualizado la asignación desde para facilitar la migración de datos
* Mejora de `SELECT ... FROM NEW/OLD TABLE` la conversión de declaraciones
* Nueva conversión de `ALTER` declaraciones para procedimientos y funciones
* Nueva conversión de asignaciones de desestructuración

## <a name="ssma-v87"></a>SSMA v8.7

La versión v8.7 de SSMA para DB2 incluye el nuevo analizador de sintaxis DB2, así como correcciones menores y mejoras de rendimiento en la interfaz gráfica de usuario.

Además, SSMA para DB2 ahora proporciona:

* Una corrección para la detección de claves externas al migrar desde DB2 en LUW.
* Se ha `SELECT ... FOR UPDATE` mejorado la conversión de la declaración.
* Se ha `COUNT` mejorado la conversión de la función en tablas MQ.
* Conversión `SAVEPOINT` de declaraciones.
* Conversión para emular el `NULL` comportamiento `ORDER BY` de DB2 para los valores de la cláusula.
* Compatibilidad de análisis para la instrucción ASSOCIATE RESULT SET.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

Además de un conjunto de correcciones de destino diseñado para mejorar la facilidad de uso y el rendimiento, la versión v8.6 de SSMA para DB2 se ha mejorado agregando una configuración que permite a los usuarios omitir las propiedades extendidas de SSMA en el código convertido.

Para aprovechar esta configuración, en SSMA para**Project Settings** > DB2, vaya a **Conversión** > **general** > **Conversion**de configuración de proyecto de herramientas y, a continuación, en **Varios**, actualice el valor de la configuración **Omitir propiedades extendidas** a **Sí**.

![Omitir configuración de propiedades extendidas](../db2/media/ssma-omit-extended-properties.png)

Además, SSMA para DB2 ahora proporciona:

* Una corrección para la conversión de funciones que utilizan valores de argumento predeterminados.
* Se ha mejorado `PARAMETER` el análisis de la cláusula para las funciones.
* La capacidad de `LEAVE` convertir la instrucción.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

La versión v8.5 de SSMA para DB2 se ha mejorado con compatibilidad con la autenticación de Azure Active Directory y compatibilidad básica con características JSON en SQL Server, junto con un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento.

Además, SSMA para DB2 se ha mejorado con:

* Compatibilidad con la `GET DIAGNOSTICS` adición de conversión para la instrucción con `ROW_NUMBER`.
* Corrección de un error relacionado con los espacios al principio del nombre del objeto que no se respeta.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

La versión v8.4 de SSMA para DB2 se mejora con correcciones de destino que están diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

> [!IMPORTANT]
> Con las versiones 7.4 de SSMA a 8.4, .NET 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v8.3

La versión v8.3 de SSMA para DB2 se mejora con correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para DB2 proporciona correcciones que:

* Abordar problemas de accesibilidad.
* Agregue compatibilidad `hierarchyid` básica para el tipo en SQL Server.
* Reemplace el uso de la función `RTRIM` / `LTRIM`TRIM en consultas de detección de z/OS por .
* Permitir al usuario especificar la colección de paquetes `NULLID`al conectarse en 'Modo estándar' (valor predeterminado es ).
* Agregar conversión para `CREATE TABLE AS SELECT`.
* Mejore las conversiones de tablas temporales globales.
* Soluciona un problema con el orden de comprobación de unicidad de objetos para priorizar las tablas sobre las restricciones, si los nombres chocan.
* Soluciona un problema con la `DATE` `TIMESTAMP` carga de los valores de columna predeterminados para y para z/OS.
* Admite caracteres de salto `NEL`de línea Unicode (también conocidos como ).
* Se solucionó un problema `RETURN TO` con la conversión de cursores con la cláusula missing.
* Agregue compatibilidad con `GOTO`etiquetas y .

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para DB2 se ha mejorado con para solucionar problemas con conexiones a Azure SQL Database desde la herramienta de consola SSMA y falta COUNT_BIG columna en la declaración de vistas durante la conversión. Además, esta versión incluye un conjunto específico de correcciones diseñadas para mejorar las métricas de calidad y conversión, así como correcciones para:

* Un problema con índices no agrupados deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.1 a v8.2. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para DB2 se ha mejorado para proporcionar correcciones dirigidas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.0 a v8.1. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para DB2 se ha mejorado para proporcionar correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancias administradas de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos destinados a Instancia administrada de Azure SQL Database:

  ![Proyecto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Asesor **fixdena**posterior a la conversión . Más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario ahora puede seleccionar bases de datos/esquemas de interés. Seleccionar solo los esquemas que planea migrar ahorrará tiempo durante la conexión inicial y mejorará el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones dirigidas diseñadas para proporcionar protecciones adicionales de seguridad y privacidad para cumplir con los cambios en los requisitos globales.
* Una solución `BEGIN-END` para la conversión de bloques.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Compatibilidad con la línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad con la migración de datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción de menú contextual con el botón derecho.
* El cuadro de diálogo de conexión de Azure SQL Database en SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para DB2 contiene los siguientes cambios:

* Cambiar asignación de tipos resaltada en *Configuración del proyecto*.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para DB2 contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* En función de la demanda popular, la versión de 32 bits de SSMA para DB2 está de vuelta. En comparación con la implementación anterior (antes de v7.4), hay dos paquetes de instalación, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible utilizar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para DB2 se ha mejorado con correcciones de destino que mejoran la calidad y las métricas de conversión y con compatibilidad con SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión v7.5 de SSMA para DB2 se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para DB2 contiene los siguientes cambios:

* La opción Tiempo de **espera** de consulta ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con correcciones específicas, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .NET 4.5.2 es un requisito previo para instalar SSMA v7.4. Además, a partir de v7.4, se ha interrumpido la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Marco de extensibilidad SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto de SQL Server Data Tools (SSDT)SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

      ![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que SSMA puede consumir para realizar conversiones personalizadas.
    * Ahora puede construir código que puede controlar las conversiones de sintaxis personalizadas y las conversiones que no se controlaban anteriormente por SSMA.
      * Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [Extending SQL Server Migration Assistant's conversion capabilities](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargue un proyecto de ejemplo para la conversión desde esta entrada de [blog.](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)

## <a name="ssma-v72"></a>SSMA v7.2

La versión v7.2 de SSMA para DB2 contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Mejoras de telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión v7.1 de SSMA para DB2 contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino compatible para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de esquemas y datos para dirigirse a los servidores SQL.
* Compatibilidad con actualizaciones automáticas para descargar la última versión de SSMA tan pronto como esté disponible.
* Los archivos binarios instalables SSMA ahora se entregan a través de archivos de paquete de Windows Installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para DB2 contiene los siguientes cambios:

* Se ha agregado compatibilidad con SQL Server 2016.
* Se ha añadido la conversión de db2 en memoria y tablas normales a características de SQL Server en memoria y hekaton.
* Se ha añadido la conversión de controles de acceso de DB2 a objetos de directiva de SQL Server (seguridad de nivel de fila para DB2).
* Se ha agregado la conversión de tablas con versiones del sistema DB2 a tablas temporales de SQL ServerSQL Server .
* Analizador y resolución DB2 mejorados.
* Se ha eliminado la comprobación del instalador de .NET 2.0.
* Se ha \*eliminado el archivo .dll innecesario del instalador de Db2.
* Corregido `save-project` `open-project` y comandos para la consola SSMA.
* Se `securepassword` ha corregido el comando para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido un error en la configuración global.
  
## <a name="march-2016"></a>marzo de 2016

La versión preliminar de marzo de 2016 de SSMA para DB2 agrega compatibilidad para la migración a SQL Server 2016.

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para DB2 contiene los siguientes cambios:
  
* Añadido soporte para una serie de funciones estándar.
* Corregidos errores del analizador DB2.
* Se ha corregido la compatibilidad con DB2 v9 zOS (RFC 5690920).
* Corregidos errores de identificador no resueltos de DB2 durante la conversión.
* Se ha añadido el elemento de menú Ver registro a SSMA (RFC 5706203).
* Se ha añadido telemetría.
  
## <a name="november-2014"></a>Noviembre de 2014

La versión de noviembre de 2014 de SSMA para DB2 fue la versión inicial.
