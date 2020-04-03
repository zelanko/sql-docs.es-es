---
title: Novedades de SSMA para MySQL (MySQLToSql) Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
ms.author: jtoland;alexiva
ms.openlocfilehash: 9d5c33bbb9e09a5a833c928547a5ec659fe43c96
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625548"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novedades de SSMA para MySQL (MySQLToSql)

En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para MySQL en cada versión.

## <a name="ssma-v88"></a>SSMA v8.8

La versión v8.8 de SSMA para MySQL incluye:

* Mejoras en la estabilidad de sincronización de objetos de SQL Server
* Mejoras en el rendimiento de la interfaz gráfica de usuario durante la evaluación y la conversión

## <a name="ssma-v87"></a>SSMA v8.7

La versión v8.7 de SSMA para MySQL tiene correcciones menores y mejoras de rendimiento en la interfaz gráfica de usuario.

Además, SSMA para MySQL `LIMIT` ahora proporciona la conversión de cláusula al tener como destino Azure SQL.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

Además de un conjunto de correcciones de destino diseñado para mejorar la facilidad de uso y el rendimiento, la versión v8.6 de SSMA para MySQL se ha mejorado agregando una configuración que permite a los usuarios omitir las propiedades extendidas de SSMA en el código convertido.

Para**Project Settings** > aprovechar esta configuración, en SSMA para MySQL, vaya **a** > **Conversión****general** > de configuración de proyecto de herramientas y, a continuación, en **Varios**, actualice el valor de la configuración **Omitir propiedades extendidas** a **Sí**.

![Omitir configuración de propiedades extendidas](../mysql/media/ssma-omit-extended-properties.png)

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

La versión v8.5 de SSMA para MySQL se ha mejorado con compatibilidad con la autenticación de Azure Active Directory y compatibilidad básica con características JSON en SQL Server, junto con un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

La versión v8.4 de SSMA para MySQL se mejora con correcciones de destino que están diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

> [!IMPORTANT]
> Con las versiones 7.4 de SSMA a 8.4, .NET 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v8.3

La versión v8.3 de SSMA para MySQL se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para MySQL proporciona correcciones que:

* Abordar problemas de accesibilidad.
* Agregue compatibilidad `hierarchyid` básica para el tipo en SQL Server.

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para MySQL se ha mejorado con un conjunto específico de correcciones diseñadas para mejorar las métricas de calidad y conversión, así como correcciones para:

* Un problema con índices no agrupados deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.1 a v8.2. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para MySQL se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.0 a v8.1. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para MySQL se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancias administradas de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos destinados a Instancia administrada de Azure SQL Database:

  ![Proyecto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

* Asesor **fixdena**posterior a la conversión . Más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario ahora puede seleccionar bases de datos/esquemas de interés. Seleccionar solo los esquemas que planea migrar ahorrará tiempo durante la conexión inicial y mejorará el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para MySQL contiene los siguientes cambios:

* Correcciones dirigidas diseñadas para proporcionar protecciones adicionales de seguridad y privacidad para cumplir con los cambios en los requisitos globales.
* Una corrección para la conversión de espacios entre el nombre de la función y la lista de argumentos.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para MySQL contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Compatibilidad parcial para migrar tipos de datos espaciales de MySQL a Azure SQL Database.
* Compatibilidad con la línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad con la migración de datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción de menú contextual con el botón derecho.
* El cuadro de diálogo de conexión de Azure SQL Database en SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para MySQL contiene los siguientes cambios:

* Cambiar la asignación de tipos resaltada en Configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para MySQL contiene los siguientes cambios:

* SSMA para MySQL se ha mejorado con correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Según la demanda popular, la versión de 32 bits de SSMA para MySQL está de vuelta. En comparación con la implementación anterior (antes de v7.4), hay dos paquetes de instalación, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible utilizar la versión de 64 bits, si es posible.
* SSMA para MySQL ahora tiene modo de conexión de cadena de conexión ODBC, que le permite utilizar cualquier controlador ODBC de terceros que son compatibles con MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para MySQL se ha mejorado con correcciones dirigidas que mejoran la calidad y las métricas de conversión y con compatibilidad con SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión v7.5 de SSMA para MySQL se ha mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para MySQL contiene los siguientes cambios:

* La opción Tiempo de **espera** de consulta ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

    ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
* La métrica de calidad y conversión se ha mejorado con correcciones específicas, en función de los comentarios de los clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para instalar SSMA v7.4. Además, a partir de v7.4, se está interrumpiendo la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para MySQL contiene los siguientes cambios:

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

La versión v7.2 de SSMA para MySQL contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Mejoras de telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión v7.1 de SSMA para MySQL contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino compatible para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de esquemas y datos para dirigirse a los servidores SQL.
* SSMA ahora admite actualizaciones automáticas para descargar la última versión de SSMA tan pronto como esté disponible.
* Los archivos binarios instalables SSMA ahora se entregan a través de archivos de paquete de Windows Installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para MySQL contiene los siguientes cambios:

* Se ha agregado compatibilidad con SQL Server 2016.
* Analizador y resolución mejorados.
* Se ha eliminado la comprobación del instalador de .NET 2.0.
* Se ha actualizado la dependencia del paquete de extensión de .NET 3.5 a .NET 4.0.
* Se ha corregido la asignación de tipos BigInt predeterminada para MySql.
* Corregido `save-project` `open-project` y comandos para la consola SSMA.
* Se `securepassword` ha corregido el comando para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido la carga de objetos MsSql.
* Se ha corregido un error en la configuración global.

## <a name="march-2016"></a>marzo de 2016

La versión preliminar de marzo de 2016 de SSMA para MySQL agrega compatibilidad para la migración a SQL Server 2016.
  
## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para MySQL contiene los siguientes cambios:

* Se ha añadido el elemento de menú Ver registro a SSMA (RFC 5706203).
* Se ha añadido telemetría.
  
## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA para MySQL contiene los siguientes cambios:
  
* Se ha mejorado la conversión de código de azure SQL DB.
* La funcionalidad del paquete de extensión se movió al esquema para admitir Azure SQL DB.
* Mejoras de rendimiento probadas para bases de datos con más de 10k objetos.
* Mejoras en la interfaz de usuario para tratar con un gran número de objetos.
* Resaltado de esquemas LOB conocidos (para que se puedan omitir en la conversión).
* Mejoras en la velocidad de conversión.
* Mostrar recuentos de objetos en la interfaz de usuario.
* Reducción del tamaño del informe en más de un 25%.
* Mensajes de error mejorados para construcciones sin analizar.
  
## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA para MySQL contiene los siguientes cambios:
  
* Se ha agregado compatibilidad con SQL Server 2014.
* Se han corregido errores relacionados con la conversión a Azure.
* Se han corregido errores relacionados con las páginas de informes invisibles en IE 10.
  
## <a name="july-2011"></a>julio de 2011

La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:
  
* Soporte para `LIMIT` la [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] `OFFSET`conversión de a .
* Se ha mejorado el informe de errores durante la migración de datos.
  
## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA para MySQL contiene los siguientes cambios:
  
* Instalación única de "SSMA para MySQL", que admite [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)], [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] y Azure SQL.
* La capacidad [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]de conectarse .
* Motor de migración de datos del lado cliente mejorado, que admite la migración paralela de datos.
* Mejora del rendimiento de la migración de datos con modelos de recuperación de registrosimple y masivo.
* SSMA para la versión de la consola de MySQL admite la compatibilidad con versiones anteriores. Puede abrir los proyectos creados por versiones anteriores a SSMA v5.0.
* SSMA para MySQL v5.0 producto se puede instalar en paralelo (SxS) con versiones anteriores del producto SSMA.
  
## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA para MySQL contiene las siguientes características:
  
**1. Mejoras en la interfaz de usuario:**

* Pestaña 'Modos SQL' para objetos de base de datos MySQL
* Pestaña 'Configuración' para objetos de base de datos MySQL
* Pestaña 'Datos' para tablas MySQL
* Configuración actualizada del proyecto en las páginas de conversión y migración
* 'Configuración de migración de datos' a nivel de tabla
  
**2. Mejoras en la conexión a MySQL y SQL Server:**
  
* Conectividad SSL en MySQL
* Conectividad cifrada en SQL Server
  
**3. Mejoras en MySQL Metabase Explorer:**
  
* Cargando todos los objetos de base de datos MySQL y sus respectivas pestañas.
  
**4. Mejoras en la conversión de objetos:**
  
* Conversión de objetos de metabase de MySQL: procedimientos, funciones, vistas, desencadenadores e instrucciones.
* Compatibilidad limitada con tipos de datos espaciales en tablas.
* Opción para convertir funciones MySQL en Procedimientos almacenados de SQL Server
* Opción para aplicar modos SQL y asignación de conjuntos de caracteres durante la conversión de objetos
  
**5. Mejoras en la migración de datos:**  
  
* Compatibilidad con la migración de datos mediante motores de migración de datos del lado del servidor y del cliente
* Soporte para la migración de datos espaciales
* SQL personalizado para la migración de datos para tablas
  
**6. SSMA para la consola MySQL:**  
  
* Característica de consola de soporte para SSMA para MySQL  
* Compatibilidad con la interfaz a nivel de script  
  
## <a name="january-2010"></a>Enero de 2010

La versión de enero de 2010 de SSMA para MySQL fue la versión inicial. Contiene las siguientes características:
  
* Se ha agregado compatibilidad para la migración a SQL Server local y Azure SQL.  
  
* **Instantánea de característica:** Migración de esquemas y datos de tablas/índices/restricciones de MySQL.
