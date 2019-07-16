---
title: Novedades de SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 20fc72ce649d8ab66c43fe1c8f3a87775d83f9fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086786"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Novedades de SSMA para Oracle (OracleToSQL)
Este artículo se enumeran los cambios de Oracle en cada versión de SQL Server Migration Assistant (SSMA).

## <a name="ssma-v82"></a>SSMA v8.2

La versión v8.2 de SSMA para Oracle se ha mejorado para:

* Agregar compatibilidad con DBMS_OUTPUT. HABILITAR O DESHABILITAR.
* Quitar CAST AS FLOAT para las columnas BINARY_FLOAT y BINARY_DOUBLE de forma predeterminada en la consulta de migración de datos.
* Corregir la actualización de las secuencias si ha cambiado el valor actual.
* Corregir el error relacionado con la interpretación incorrecta de pseudocolumnas (ROWNUM, etc.) si existe una columna con el mismo nombre.
* Corregido un bloqueo que se produce convertir BUCLES con identificador sin resolver ambiguo.

Además, esta versión incluye un conjunto de correcciones diseñado para mejorar la calidad y las métricas de conversión, así como correcciones de destino:

* Un problema con los índices no clúster deshabilitados tras la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.1 a v8.2. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>V8.1 SSMA

La versión v8.1 de SSMA para Oracle se ha mejorado con correcciones de destino que están diseñadas para mejorar las métricas de calidad y la conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.0 a v8.1. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para Oracle se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y la conversión de las métricas. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **Azure SQL Database Managed Instance** como destino. Ahora puede crear nuevos proyectos destinados a la instancia administrada de Azure SQL Database:

  ![Proyecto de base de datos de SQL para MI](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > SSMA para Oracle: paquete de extensión también se actualizó para permitir que las instalaciones remotas de la instancia administrada de Azure SQL Database:
  >
  > ![SSMA para Oracle: paquete de extensión](../media/ssma-oracle-ext-pack.png)

  No se admiten algunas características, incluida la migración de datos de evaluador y del lado servidor, cuando el destino es la instancia administrada de Azure SQL Database. Obtenga más información sobre [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/).

* Después de la conversión **corrección advisor**. Más información sobre él [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección de base de datos/esquema preliminar.

  Al conectarse al origen, el usuario ahora puede seleccionar las bases de datos y esquemas de interés. Seleccionar sólo los esquemas que se va a migrar ahorrará tiempo durante la conexión inicial y mejorar el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

* La capacidad para usar el controlador de red oficial, administrado para conectarse a Oracle. El controlador OCI ya no es un requisito previo para utilizar SQL Server Migration Assistant para Oracle.

* La capacidad para asignar ROWID y UROWID a VARCHAR de forma predeterminada. Ha cambiado de 'uniqueidentifier' para dar cabida a la migración de datos para columnas ROWID explícitas.

## <a name="ssma-v710"></a>SSMA v7.10

La versión v7.10 de SSMA para Oracle contiene los siguientes cambios:

* Diseñado para proporcionar seguridad adicional y protecciones de seguridad para satisfacer los cambios en los requisitos globales correcciones de destino.
* Una mejora de la conversión relacionados con consultas jerárquicas.

## <a name="ssma-v79"></a>SSMA v7.9

La versión v7.9 de SSMA para Oracle contiene los siguientes cambios:

* Correcciones de destino que mejoran las métricas de calidad y la conversión.
* Compatibilidad con las instrucciones "Continue" migrar desde Oracle a SQL Server.
* Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Soporte técnico para migrar datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción del menú contextual.
* El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión v7.8 de SSMA para Oracle contiene los siguientes cambios:

* Compatibilidad con:
  * Expresión de fila para la cláusula IN.
  * Conversiones de tipos implícita.
  * Conversión de UID para Azure SQL Database.
* Cambiar la asignación de tipos de resaltado en la configuración del proyecto.
* La capacidad de los usuarios deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión v7.7 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión.
* Según la demanda popular, la versión de 32 bits de SSMA para Oracle es de nuevo. En comparación con la implementación anterior (antes v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.
* Compatibilidad con SQL Server 2017 ahora es oficial con el paquete de extensiones de Oracle también se admiten en Linux (nueva opción de instalación remota). Tenga en cuenta que la funcionalidad del módulo de extensión está limitada cuando se instala en Linux, como la herramienta de comprobación y no se admiten las características de migración de datos del servidor.
* SSMA para Oracle le permite migrar vistas materializadas como tablas normales (configurables a través de la configuración del **configuración del proyecto** -> **sincronización**  ->  **Detectar tablas de copia de seguridad de las vistas materializadas**).

## <a name="ssma-v76"></a>SSMA v7.6

La versión v7.6 de SSMA para Oracle se ha mejorado con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión 7.5 de SSMA para Oracle contiene los siguientes cambios:

* Mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.
* Actualizado para mejorar la métrica de calidad y la conversión con correcciones de destino, como la mejora del tratamiento de tipos de datos de fecha y float durante la migración de datos, según los comentarios recibidos.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para Oracle contiene los siguientes cambios:

* SSMA para Oracle ahora es compatible con Azure SQL Data Warehouse como una plataforma de destino para la migración.

  ![Ventana nuevo proyecto](../media/new-project.png)
  * Es compatible con las opciones de almacenamiento del almacén de datos tal como se muestra en la siguiente imagen:

  ![Opciones de almacenamiento para almacenamiento de datos](../media/storage-options_red.png)
  * Admite las opciones de distribución de datos tal como se muestra en la siguiente imagen:

  ![distribución de datos del almacén de datos](../media/data-distribution_red.png)

* El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

* La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para Oracle contiene los siguientes cambios:

* Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
* Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  * Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    * Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicional e implementar la base de datos.

      ![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que pueden utilizarse en SSMA para realizar conversiones personalizadas.
    * Ahora se puede crear código que pueda controlar las conversiones de sintaxis personalizada y las conversiones que antes no estaban controlaba SSMA.
      * Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión de ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargar un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v7.2

La versión v7.2 de SSMA para Oracle contiene los siguientes cambios:

* Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
* Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión 7.1 de SSMA para Oracle contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y esquema para servidores SQL Server de destino.
* SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto está disponible.
* Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

## <a name="may-2016"></a>Mayo de 2016

La versión de mayo de 2016 de SSMA para Oracle contiene los siguientes cambios:  

* Se agregó compatibilidad para SQL Server 2016.
* Se ha agregado conversión Oracle flashback de tablas de almacenamiento a las tablas temporales de SQL Server.

  > [!NOTE]
  > SSMA no copia datos del historial de las tablas de almacenamiento de datos Flashback de Oracle. Como resultado, los datos del historial se deben copiar manualmente durante el proceso de migración. Además, aunque SSMA no muestra la tabla de historial en el Explorador de metadatos de SQL Server porque se trata como una tabla del sistema, puede ver la tabla de historial en SQL Server Management Studio.
  >
  > SQL Server 2016 no admite varias características de Oracle Flashback, como:
  >
  > * Consulta de transacciones de Oracle Flashback
  > * Paquete DBMS_FLASHBACK
  > * Transacción Flashback
  > * Archivo de datos Flashback
  > * Tabla Flashback
  > * Colocar Flashback
  > * Base de datos Flashback
* Se ha agregado conversión de Oracle VPD directiva a los objetos de directiva de SQL Server (seguridad de nivel de fila para Oracle).
* Un menor tiempo de carga inicial para Oracle.
* Analizador mejorada y la resolución.
* Quitar la comprobación de instalador para .net 2.0.
* Dependencia del módulo de extensión actualizado de .net 3.5 a .net 4.0.
* Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
* Se ha corregido el comando "securepassword" para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Se ha corregido la conversión de tipos de datos de caracteres para Oracle.
* Se corrigió el error en la configuración global.
  
## <a name="march-2016"></a>Marzo de 2016

La versión de vista previa de marzo de 2016 de SSMA para Oracle se ha agregado compatibilidad con:  
  
* Migración a SQL Server 2016.  
* ¡¡¡¡Migrar la seguridad de nivel de fila de Oracle (con algunas limitaciones).  
* Migración de Oracle en las tablas en memoria para SQL Server columna Store.  
  
## <a name="january-2016"></a>Enero de 2016

La de enero de 2014 versión de mantenimiento de SSMA para Oracle contiene los siguientes cambios:  
  
* Se agregó compatibilidad para los índices clúster.  
* Se ha corregido consultas lentas de esquema Oracle (RFC 5076207).  
* Fijo conectarse a Azure desde la consola.  
* La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203). 
* Se ha agregado telemetría.
  
## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
* Se agregó compatibilidad para la base de datos de SQL Azure.
* Funcionalidad del módulo de extensión se mueve al esquema para admitir la base de datos de SQL Azure.
* Se agregó compatibilidad para las vistas materializadas de Oracle.  
* Tablas con optimización para memoria de SQL Server 2014 se agregó compatibilidad con.  
* Mejoras de rendimiento incluida en las pruebas de bases de datos con más de 10k objetos.  
* Se ha agregado mejoras de interfaz de usuario para tratar con un gran número de objetos.  
* Agregar resaltado de esquemas LOB "conocidos".  
* Incluye mejoras en la velocidad de conversión.  
* Se ha agregado compatibilidad para mostrar el objeto de cuenta en la interfaz de usuario.  
* Tamaño del informe reducida en más del 25%.
* Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
* Se agregó compatibilidad de MS SQL Server 2014.  
* Se agregó compatibilidad de optimización de consulta y Oracle 12.  
* Errores corregidos con respecto a la conversión a Azure.  
* Errores corregidos con respecto a las páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012

La versión de enero de 2012 de SSMA para Oracle agrega compatibilidad para el tipo de fila y los parámetros de entrada RecordType su valor predeterminado es NULL.  
  
## <a name="july-2011"></a>Julio de 2011

La versión de julio de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
* Agrega compatibilidad para la conversión de la secuencia de Oracle que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generador de secuencia de "Denali".
* Durante la migración de datos de informes de errores mejorado.  
* Conversión mejorada de instrucción con palabras reservadas.  
* Mejorar la conversión implícita del valor de fecha en una función.  
  
## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
* Producto "SSMA para Oracle" consolidada, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".
* Agrega compatibilidad para conectar y migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Motor de migración mejorada de los datos del lado cliente, que admiten la migración paralela de datos.  
* Rendimiento de la migración de datos mejorada con Simple y masiva registra los modelos de recuperación.  
* Se agregó compatibilidad para la compatibilidad con versiones anteriores de los proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
* Agrega la capacidad de instalar SSMA para Oracle v5.0 productos en paralelo (SxS) con versiones anteriores de SSMA (v4.0 y v4.2).
* Se agregó compatibilidad para informar sobre los tipos definidos por el usuario (incluye el subtipo, VARRAY, tabla anidada, tabla de objetos y vista de objetos) y sus usos en bloques de PL/SQL con mensajes de error especiales.  

## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA para Oracle agregado:

* Compatibilidad con la migración a SQL Server 2008 R2.  
* Una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.  
* Compatibilidad con migración de datos con el servidor y motores de migración de datos del lado cliente.  
* Compatibilidad con la instrucción "SELECT" Custom"en la migración de datos.  
* Compatibilidad con la migración desde Oracle 11g R2.  
  
## <a name="june-2008"></a>Junio de 2008

La versión de junio de 2008 de SSMA para Oracle contiene los siguientes cambios:  
  
* Se ha agregado mejoras en el informe de evaluación, incluidos información adicional de sinónimos, origen sin procesar para la persistencia del diseño, paneles y eliminación del logotipo de SQL Server y se puede analizar objetos.  
* Se ha agregado mejoras en la conversión de objetos:  
  * Paquetes DBMS_LOB, conversión DBMS_SQL agregado.  
  * Une la conversión revisado.  
  * Modificación de las colecciones y los registros de conversión, ahora la conversión de registros en los casos más sencillos publicados a través de variables independientes para cada campo.  
  * Mejoras de implementación de registros y las colecciones.  
  * Funciones de agregación basadas en ventanas agregadas.  
  * Agrega la cláusula de cubo o el paquete acumulativo de actualizaciones.  
  * Mejora para NEXTVAL/CURVAL.  
  * Se han agregado las columnas de agrupación en la cláusula SET, conjuntos de agrupamiento y el Id. de agrupación.  
  * COMBINAR la instrucción agregado.  
  * Compatibilidad con nuevos tipos de fecha y hora y conversión de registros y las colecciones como tipos de datos CLR agregados.  
* Se agregaron nuevas características de evaluador. Tablas ahora se pueden probar como objetos mediante la herramienta de comprobación, se puede modificar un orden de llamada de varios objetos apta para las pruebas en caso de prueba, usuario puede probar los procedimientos y funciones con registros y las colecciones como parámetros y valores devueltos y se ha agregado un analizador de dependencias para comprobar solo tablas usadas.  
  
## <a name="august-2007"></a>Agosto de 2007

La versión de agosto de 2007 de SSMA para Oracle agregado:

* Un nuevo componente de EVALUADOR le permite crear, administrar y ejecutar casos de prueba para comprobar el código convertido de SQL.  
* Se han agregado al convertidor de SQL admite la conversión de módulos locales, colecciones y subtipos de Oracle.  
* Una nueva característica de sincronización le permite sincronizar objetos específicos con la base de datos de SQL Server.  
* Nuevas opciones de conversión.  
  
## <a name="april-2007"></a>Abril de 2007

La versión de abril de 2007 de SSMA para Oracle fue la versión inicial.
