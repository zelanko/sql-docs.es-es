---
title: Novedades de SSMA para Oracle (OracleToSQL) Microsoft Docs
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: jtoland;alexiva
ms.openlocfilehash: 88b87aad931f28637accc95aa4d993037fcf0b0a
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625597"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Novedades de SSMA para Oracle (OracleToSQL)

En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para Oracle en cada versión.

## <a name="ssma-v88"></a>SSMA v8.8

La versión v8.8 de SSMA para Oracle incluye:

* Mejoras en la estabilidad de sincronización de objetos de SQL Server
* Mejoras en el rendimiento de la interfaz gráfica de usuario durante la evaluación y la conversión
* Mejora de `OVER PARTITION` la conversión de cláusulas analíticas
* Nueva conversión para `LEAD` la función analítica
* Nueva conversión para cláusulas de factorización de subconsultas
* Nueva `REPLICATE` opción de distribución para Azure SQL Data Warehouse
* Nuevo analizador de sintaxis Oracle para mejorar aún más el rendimiento de las conversiones

## <a name="ssma-v87"></a>SSMA v8.7

La versión v8.7 de SSMA para Oracle tiene correcciones menores y mejoras de rendimiento en la interfaz gráfica de usuario.

Además, SSMA para Oracle ahora permite filtrar objetos en función del estado de validez en el cuadro de diálogo 'Selección avanzada de objetos'.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v86"></a>SSMA v8.6

Además de un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento, la versión v8.6 de SSMA para Oracle se ha mejorado agregando una configuración que permite a los usuarios omitir las propiedades extendidas de SSMA en el código convertido.

Para aprovechar esta configuración, en SSMA para Oracle, vaya a**Project Settings** >  **Conversión** > **general** > **Conversion**de configuración de proyecto de herramientas y, a continuación, en **Varios**, actualice el valor de la configuración **Omitir propiedades extendidas** a **Sí**.

![Omitir configuración de propiedades extendidas](../oracle/media/ssma-omit-extended-properties.png)

Además, SSMA para Oracle ahora proporciona `XMLTABLE` un análisis mejorado de la cláusula.

> [!IMPORTANT]
> Con SSMA v8.5 y versiones posteriores, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v85"></a>SSMA v8.5

La versión v8.5 de SSMA para Oracle se ha mejorado con compatibilidad con la autenticación de Azure Active Directory y compatibilidad básica con características JSON en SQL Server, junto con un conjunto específico de correcciones diseñadas para mejorar la facilidad de uso y el rendimiento.

Además, SSMA para Oracle se ha mejorado con soporte para:

* Limitar el número de objetos seleccionados para la `WHERE .. IN (..)` detección a 990 (el límite de cláusula de Oracle es 1000 elementos).
* Migración `RAW` de `UNIQUEIDENTIFIER`datos de a .
* Análisis de `PARALLEL_ENABLE` cláusula.

Por último, la versión v8.5 de SSMA para Oracle ahora proporciona:

* Se ha mejorado el rendimiento de las constantes empaquetadas convertidas.
* Una actualización para Oracle Data Provider para .NET a la versión 19.5.0.

> [!IMPORTANT]
> Con SSMA v8.5, .NET 4.7.2 es un requisito previo de instalación. Si necesita instalar esta versión, puede descargar el archivo en tiempo de ejecución desde [aquí.](https://dotnet.microsoft.com/download/dotnet-framework/net472)

## <a name="ssma-v84"></a>SSMA v8.4

La versión v8.4 de SSMA para Oracle se mejora con correcciones de destino que están diseñadas para solucionar problemas de accesibilidad y corregir un error relacionado con las columnas de índice máximo (para permitir 32 en lugar de 16) para SQL Server 2016 y versiones posteriores.

Además, esta versión de SSMA `SYS_REFCURSOR` para `OUT` Oracle agrega la conversión para como parámetros de procedimiento almacenado.

> [!IMPORTANT]
> Con las versiones 7.4 a 8.4 de SSMA, .NET 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v83"></a>SSMA v8.3

La versión v8.3 de SSMA para Oracle se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para Oracle proporciona correcciones que:

* Abordar problemas de accesibilidad.
* Agregue compatibilidad `hierarchyid` básica para el tipo en SQL Server.
* Se soluciona un problema con un tipo de valor devuelto desconocido para una función a la que se llama a través de un sinónimo.
* Actualice ODP.NET a v19.3.

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para Oracle se ha mejorado para:

* Agregue compatibilidad `DBMS_OUTPUT.ENABLE` / `DISABLE`con .
* Quitar `CAST AS FLOAT` `BINARY_FLOAT` y `BINARY_DOUBLE` columnas en la consulta de migración de datos predeterminada.
* Las secuencias de corrección se actualizan si el valor actual ha cambiado.
* Se ha corregido un error relacionado`ROWNUM`con la interpretación incorrecta de pseudocolumnas ( , etc.) si existe una columna con el mismo nombre.
* Se ha corregido un `FOR` bloqueo que se produce la conversión de bucles con un identificador ambiguo sin resolver.

Además, esta versión incluye un conjunto específico de correcciones diseñadas para mejorar las métricas de calidad y conversión, así como correcciones para:

* Un problema con índices no agrupados deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.1 a v8.2. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v81"></a>SSMA v8.1

La versión v8.1 de SSMA para Oracle se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede provocar el error de una actualización de SSMA v8.0 a v8.1. Si encuentra este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para Oracle se ha mejorado con correcciones específicas diseñadas para mejorar la calidad y las métricas de conversión. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **instancias administradas de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos destinados a Instancia administrada de Azure SQL Database:

  ![Proyecto SQL DB MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > El Paquete de extensión SSMA para Oracle también se actualizó para permitir instalaciones remotas en Instancia administrada de Azure SQL Database:
  >
  > ![SSMA para Oracle Extension Pack](../media/ssma-oracle-ext-pack.png)

  Algunas características, como el Probador y la migración de datos del lado del servidor, no se admiten al tener como destino Instancia administrada de Azure SQL Database. [Aquí encontrará más información](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* Asesor **fixdena**posterior a la conversión . Más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario ahora puede seleccionar bases de datos/esquemas de interés. Seleccionar solo los esquemas que planea migrar ahorrará tiempo durante la conexión inicial y mejorará el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

* La capacidad de utilizar el controlador oficial de .NET administrado para conectarse a Oracle. El controlador OCI ya no es un requisito previo para usar SQL Server Migration Assistant para Oracle.

* La capacidad `ROWID` de `UROWID` `VARCHAR` asignar y de forma predeterminada. Se `uniqueidentifier` ha cambiado de `ROWID` para dar cabida a la migración de datos para columnas explícitas.

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para Oracle contiene los siguientes cambios:

* Correcciones dirigidas diseñadas para proporcionar protecciones adicionales de seguridad y privacidad para cumplir con los cambios en los requisitos globales.
* Mejora de la conversión relacionada con consultas jerárquicas.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para Oracle contiene los siguientes cambios:

* Correcciones dirigidas que mejoran la calidad y las métricas de conversión.
* Compatibilidad con la migración de instrucciones "Continuar" de Oracle a SQL Server.
* Compatibilidad con la línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad con la migración de datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción de menú contextual con el botón derecho.
* El cuadro de diálogo de conexión de Azure SQL Database en SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para Oracle contiene los siguientes cambios:

* Soporte para:
  * Expresión de `IN` fila para la cláusula.
  * Conversiones de tipo implícitas.
  * `UID`conversión para Azure SQL Database.
* Cambiar asignación de tipos resaltada en **Configuración del proyecto**.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle se ha mejorado con correcciones específicas que mejoran la calidad y las métricas de conversión.
* Según la demanda popular, la versión de 32 bits de SSMA para Oracle está de vuelta. En comparación con la implementación anterior (antes de v7.4), hay dos paquetes de instalación, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible utilizar la versión de 64 bits, si es posible.
* La compatibilidad con SQL Server 2017 ahora es oficial con Oracle Extension Pack compatible también con Linux (nueva opción de instalación remota). Tenga en cuenta que la funcionalidad del paquete de extensión es limitada cuando se instala en Linux, ya que no se admiten las características de migración de datos del lado del servidor y del probador.
* SSMA para Oracle permite migrar vistas materializadas como tablas normales (configurable a través de la configuración de **configuración** -> de proyecto -> **Descopia de tablas de respaldo para vistas materializadas**).**Synchronization**

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para Oracle se ha mejorado con correcciones específicas que mejoran la calidad y las métricas de conversión y con compatibilidad con SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión v7.5 de SSMA para Oracle contiene los siguientes cambios:

* Mejorado con varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.
* Se ha actualizado para mejorar la métrica de calidad y conversión con correcciones dirigidas, como un mejor control de los tipos de datos de fecha y flotante durante la migración de datos, en función de los comentarios de los clientes.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle ahora admite Azure SQL Data Warehouse como plataforma de destino para la migración.

  ![Ventana Nuevo proyecto](../media/new-project.png)
  * Admite las opciones de almacenamiento de Data Warehouse como se muestra en la siguiente imagen:

  ![opciones de almacenamiento para el almacenamiento de datos](../media/storage-options_red.png)
  * Admite las opciones de distribución de datos como se muestra en la siguiente imagen:

  ![distribución de datos para el almacenamiento de datos](../media/data-distribution_red.png)

* La opción Tiempo de **espera** de consulta ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y conversión se ha mejorado con correcciones específicas, en función de los comentarios de los clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para instalar SSMA v7.4. Además, a partir de v7.4, se está interrumpiendo la versión de 32 bits de SSMA.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para Oracle contiene los siguientes cambios:

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

La versión v7.2 de SSMA para Oracle contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones específicas basadas en los comentarios de los clientes.
* Mejoras de telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión v7.1 de SSMA para Oracle contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino compatible para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de esquemas y datos para dirigirse a los servidores SQL.
* SSMA ahora admite actualizaciones automáticas para descargar la última versión de SSMA tan pronto como esté disponible.
* Los archivos binarios instalables SSMA ahora se entregan a través de archivos de paquete de Windows Installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para Oracle contiene los siguientes cambios:

* Se ha agregado compatibilidad con SQL Server 2016.
* Se ha añadido la conversión de tablas de archivado flashback de Oracle a tablas temporales de SQL ServerSQL Server .

  > [!NOTE]
  > SSMA no copia los datos del historial de las tablas de Oracle Flashback Data Archive. Como resultado, los datos del historial se deben copiar manualmente durante el proceso de migración. Además, aunque SSMA no muestra la tabla de historial en el explorador de metadatos de SQL Server porque se trata como una tabla del sistema, puede ver la tabla de historial en SQL Server Management StudioSQL Server Management Studio.
  >
  > SQL Server 2016 no admite varias características de Oracle Flashback, entre las que se incluyen:
  >
  >   * Oracle Flashback Transaction Query
  >   * `DBMS_FLASHBACK`Paquete
  >   * Transacción Flashback
  >   * Flashback Data Archive
  >   * Mesa Flashback
  >   * Flashback Drop
  >   * Base de datos Flashback

* Se ha añadido la conversión de oracle VPD Policy a objetos de directiva de SQL Server (seguridad de nivel de fila para Oracle).
* Disminución del tiempo de carga inicial para Oracle.
* Analizador y resolución mejorados.
* Se ha eliminado la comprobación del instalador de .NET 2.0.
* Se ha actualizado la dependencia del paquete de extensión de .NET 3.5 a .NET 4.0.
* Corregido `save-project` `open-project` y comandos para la consola SSMA.
* Se `securepassword` ha corregido el comando para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido la conversión de tipos de datos de caracteres para Oracle.
* Se ha corregido un error en Configuración global.

## <a name="march-2016"></a>marzo de 2016

La versión preliminar de marzo de 2016 de SSMA para Oracle agregó compatibilidad para:

* Migración a SQL Server 2016.
* Migración de Oracle Row Level Security (con algunas limitaciones).
* Migración de Oracle en tablas de memoria al almacén de columnas de SQL ServerSQL Server .

## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2014 de SSMA para Oracle contiene los siguientes cambios:

* Se ha añadido compatibilidad con índices agrupados.
* Se han corregido las consultas de esquema de Oracle lentas (RFC 5076207).
* Se ha corregido la conexión a Azure desde la consola.
* Se ha añadido el elemento de menú Ver registro a SSMA (RFC 5706203).
* Se ha añadido telemetría.

## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA para Oracle contiene los siguientes cambios:

* Se ha agregado compatibilidad con Azure SQL DB.
* La funcionalidad del paquete de extensión se movió al esquema para admitir Azure SQL DB.
* Se ha añadido compatibilidad con las vistas de Oracle Materialized.
* Se ha agregado compatibilidad con tablas optimizadas para memoria de SQL Server 2014.
* Se incluyeron mejoras de rendimiento probadas para bases de datos con más de 10k objetos.
* Se han añadido mejoras en la interfaz de usuario para tratar con un gran número de objetos.
* Se ha añadido resaltado de esquemas LOB conocidos.
* Mejoras en la velocidad de conversión incluidas.
* Se ha añadido compatibilidad para mostrar los recuentos de objetos en la interfaz de usuario.
* Se ha reducido el tamaño del informe en más de un 25%.
* Mensajes de error mejorados para construcciones sin analizar.

## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA para Oracle contiene los siguientes cambios:

* Se ha agregado compatibilidad con MS SQL Server 2014.
* Se ha añadido compatibilidad con Oracle 12 y optimización de consultas.
* Se han corregido errores relacionados con la conversión a Azure.
* Se han corregido errores relacionados con las páginas de informes invisibles en IE 10.

## <a name="january-2012"></a>enero de 2012

La versión de enero de 2012 de `RowType` `RecordType` SSMA para `NULL`Oracle agrega compatibilidad y parámetros de entrada predeterminados a .

## <a name="july-2011"></a>julio de 2011

La versión de julio de 2011 de SSMA para Oracle contiene los siguientes cambios:

* Se ha añadido compatibilidad [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] para la conversión de secuencia de Oracle al generador de secuencias.
* Se ha mejorado el informe de errores durante la migración de datos.
* Se ha mejorado la conversión de la declaración mediante palabras reservadas.
* Se ha mejorado la conversión implícita del valor de fecha en una función.

## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA para Oracle contiene los siguientes cambios:

* Producto consolidado "SSMA for Oracle", [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]que soporta [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)]y .
* Se ha añadido compatibilidad [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]para conectar y migrar a .
* Motor de migración de datos del lado cliente mejorado, que admite la migración paralela de datos.
* Se ha mejorado `Simple` `Bulk` el rendimiento de la migración de datos con los modelos de recuperación registrados y los.
* Se ha agregado compatibilidad con la compatibilidad con versiones anteriores de proyectos creados por versiones anteriores de SSMA (v4.0 y v4.2).
* Se ha añadido la capacidad de instalar SSMA para el producto Oracle v5.0 en paralelo (SxS) con versiones anteriores de SSMA (v4.0 y v4.2).
* Se ha añadido compatibilidad para notificar tipos `VARRAY` `NESTED TABLE`definidos por el usuario (incluye subtipo, , tabla de objetos y vista de objeto) y sus usos en bloques PL/SQL con mensajes de error especiales.

## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA para Oracle añadió:

* Compatibilidad con la migración a SQL Server 2008 R2.
* Una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.
* Compatibilidad con la migración de datos mediante motores de migración de datos del lado del servidor y del lado cliente.
* Compatibilidad con la instrucción "Custom SELECT" en la migración de datos.
* Compatibilidad con la migración desde Oracle 11g R2.

## <a name="june-2008"></a>Junio de 2008

La versión de junio de 2008 de SSMA para Oracle contiene los siguientes cambios:

* Se han añadido mejoras en el informe de evaluación, incluida información adicional para sinónimos, origen sin procesar para objetos analizables, paneles y eliminación de logotipos de SQL ServerSQL Server y persistencia del diseño.
* Mejoras añadidas en la conversión de objetos:
  * `DBMS_LOB`Paquetes `DBMS_SQL` , conversión agregada.
  * Se ha revisado la conversión.
  * Modificación de colecciones y conversión de registros, ahora conversión de registros en casos simples liberados a través de variables separadas para cada campo.
  * Mejoras de la implementación de registros y colecciones.
  * Se han añadido funciones de agregación de ventanas.
  * `ROLLUP`/`CUBE`cláusula añadida.
  * Mejora `NEXTVAL` / `CURVAL`para .
  * Se agregaron columnas que se agrupan en `SET` cláusula, conjuntos de agrupación e identificador de agrupación.
  * `MERGE`declaración añadida.
  * Compatibilidad con nuevos tipos de fecha y hora y conversión de registros y colecciones a medida que se agregan tipos de datos CLR.
* Se han añadido nuevas características de Tester. Las tablas ahora se pueden probar como objetos mediante Tester, se puede modificar un orden de llamada de varios objetos comprobables en caso de prueba, el usuario puede probar procedimientos y funciones con registros y colecciones como parámetros y valores devueltos, y se agregó un analizador de dependencias para comprobar solo las tablas utilizadas.
  
## <a name="august-2007"></a>Agosto de 2007

La versión de agosto de 2007 de SSMA para Oracle añadió:

* Un nuevo componente Tester le permite crear, administrar y ejecutar casos de prueba para comprobar el código SQL convertido.
* Se ha agregado compatibilidad con la conversión de subtipos, colecciones y módulos locales de Oracle al convertidor SQL.
* Una nueva característica de sincronización le permite sincronizar objetos específicos con la base de datos de SQL Server.
* Nuevas opciones de conversión.
  
## <a name="april-2007"></a>Abril de 2007

La versión de abril de 2007 de SSMA para Oracle fue la versión inicial.
