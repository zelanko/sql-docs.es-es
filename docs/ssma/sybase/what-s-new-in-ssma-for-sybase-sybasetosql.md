---
title: Novedades de SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 4da3fa07c4cdcdf2f3666c3bf85ba3669eb7e5bf
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632056"
---
# <a name="whats-new-in-ssma-for-sap-ase-sybasetosql"></a>Novedades de SSMA para SAP ASE (SybaseToSQL)
En este artículo se enumeran los cambios de SQL Server Migration Assistant (SSMA) para SAP ASE (anteriormente SSMA para Sybase) en cada versión.

## <a name="ssma-v83"></a>SSMA v 8.3

El lanzamiento de la versión 8.3 de SSMA para SAP ASE se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión de SSMA para SAP ASE proporciona correcciones que:

* Solucionar problemas de accesibilidad
* Agregar compatibilidad básica para el tipo ' hierarchyid ' en SQL Server

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v82"></a>SSMA v 8.2

La versión v 8.2 de SSMA para SAP ASE se ha mejorado con un conjunto de correcciones diseñado para mejorar la calidad y las métricas de conversión, así como las correcciones para:

* Un problema con los índices no clúster deshabilitados después de la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.1 a v 8.2. Si se produce este error, descargue la nueva versión e instálela manualmente.

> [!IMPORTANT]
> Con SSMA v 7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>SSMA v 8.1

La versión v 8.1 de SSMA para SAP ASE se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir un error en una actualización de SSMA v 8.0 a v 8.1. Si se produce este error, descargue la nueva versión e instálela manualmente.

## <a name="ssma-v80"></a>SSMA v 8.0

La versión 8.0 de SSMA para SAP ASE se ha mejorado con las correcciones de destino diseñadas para mejorar la calidad y las métricas de conversión. Además, esta versión ofrece las siguientes características nuevas:

* Compatibilidad con **instancia administrada de Azure SQL Database** como destino. Ahora puede crear nuevos proyectos que tengan como destino Instancia administrada de Azure SQL Database:

  ![Proyecto de MI de base de SQL](../media/ssma-newproject-sqldbmi.png)

* **Asesor de corrección**posterior a la conversión. Obtenga más información [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección preliminar de base de datos/esquema.

  Al conectarse al origen, el usuario puede seleccionar las bases de datos o los esquemas de interés. Si selecciona solo los esquemas que va a migrar, se ahorrará tiempo durante la conexión inicial y se mejorará el rendimiento global de SSMA.

  ![SSMA (objetos de filtro)](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v 7.10

La versión v 7.10 de SSMA para SAP ASE se ha mejorado con las correcciones de destino diseñadas para proporcionar protección adicional de seguridad y privacidad para satisfacer los cambios en los requisitos globales.

## <a name="ssma-v79"></a>SSMA v 7.9

La versión v 7.9 de SSMA para SAP ASE contiene los siguientes cambios:

* Correcciones dirigidas que mejoran las métricas de calidad y conversión.
* Compatibilidad en la línea de comandos de SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Compatibilidad para la migración de datos con SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante el uso de una opción del menú contextual.
* También se ha modificado el cuadro de diálogo de conexión Azure SQL Database en SSMA para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo Azure SQL Database tenía que mencionarse explícitamente dentro de la configuración de los proyectos.

## <a name="ssma-v78"></a>SSMA v 7.8

La versión v 7.8 de SSMA para SAP ASE contiene los siguientes cambios:

* Cambiar la asignación de tipos resaltada en la configuración del proyecto.
* La capacidad de los usuarios de deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v 7.7

La versión v 7.7 de SSMA para SAP ASE contiene los siguientes cambios:

* SSMA for SAP ASE se ha mejorado con correcciones de destino que mejoran la calidad y las métricas de conversión.
* En función de la demanda popular, la versión de 32 bits de SSMA para SAP ASE vuelve a ser. En comparación con la implementación anterior (antes de v 7.4), hay dos paquetes de instalador, pero no se pueden instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tenga. Siempre es preferible usar la versión de 64 bits, si es posible.

## <a name="ssma-v76"></a>SSMA v 7.6

La versión v 7.6 de SSMA for SAP ASE contiene los siguientes cambios:

* Correcciones de destino que mejoran las métricas de calidad y conversión y admiten SQL Server 2017 (versión preliminar pública). La compatibilidad con SQL Server 2017 en Windows y Linux está en versión preliminar pública y no debe usarse para migraciones de producción.
* Compatibilidad con la conversión de funciones de Sybase.

## <a name="ssma-v75"></a>SSMA v 7.5

La versión v 7.5 de SSMA para SAP ASE (anteriormente SSMA para Sybase) contiene los cambios siguientes:

* Varias mejoras para garantizar una mayor accesibilidad para las personas con discapacidades.
* Compatibilidad con la sintaxis de CREATE o Replace.

## <a name="ssma-v74"></a>SSMA v 7.4

La versión v 7.4 de SSMA para Sybase contiene los siguientes cambios:

* La opción **tiempo de espera de consulta** ahora está disponible durante la detección de objetos de esquema en el origen y el destino.

  ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
* La métrica de calidad y conversión se ha mejorado con las correcciones de destino, en función de los comentarios de los clientes.

  > [!IMPORTANT]
  > .Net 4.5.2 es un requisito previo para instalar SSMA v 7.4. Además, a partir de v 7.4, se suspende la versión de 32 bits de SSMA.  

## <a name="ssma-v73"></a>SSMA v 7.3

La versión v 7.3 de SSMA para Sybase contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* El marco de extensibilidad de SSMA expuesto a través de los siguientes elementos:
  * Exportar funcionalidad a un proyecto SQL Server Data Tools (SSDT).
    * Ahora puede exportar scripts de esquema de SSMA a un proyecto de SSDT. Puede usar los scripts de esquema para realizar cambios de esquema adicionales e implementar la base de datos.

        ![Comando Guardar como proyecto de SSDT](../media/export-schema-scripts_red.png)
  * Bibliotecas que puede usar SSMA para realizar conversiones personalizadas.
    * Ahora puede construir código que pueda controlar las conversiones de sintaxis personalizadas y las conversiones que no se administraron previamente mediante SSMA.
      * En esta entrada de blog se ofrecen instrucciones sobre cómo construir un convertidor personalizado, que amplían las [capacidades de conversión de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      * Descargue un proyecto de ejemplo para la conversión de esta [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

## <a name="ssma-v72"></a>SSMA v 7.2

La versión v 7.2 de SSMA para Sybase contiene los siguientes cambios:

* Métrica de calidad y conversión mejorada con correcciones de destino basadas en los comentarios de los clientes.
* Mejoras en la telemetría para proporcionar mejores puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v 7.1

La versión v 7.1 de SSMA para Sybase contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 es ahora una plataforma de destino admitida para la migración. Esta característica se encuentra en Technical Preview y admite el movimiento de datos y esquemas para los servidores SQL Server de destino.
* Compatibilidad con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto esté disponible.
* Los binarios instalables de SSMA se entregan ahora a través de los archivos de paquete de Windows Installer (. msi).

## <a name="may-2016"></a>2016 de mayo

La versión de mayo de 2016 de SSMA para Sybase contiene los siguientes cambios:  

* Compatibilidad agregada para SQL Server 2016.
* Se quitó la comprobación del instalador para .net 2,0.
* Dependencia del paquete de extensiones actualizada de .net 3,5 a .net 4,0.
* Se han corregido los comandos "guardar proyecto" y "Abrir proyecto" para la consola de SSMA.
* Se corrigió el comando "securepassword" para la consola de SSMA.
* Recuento fijo de objetos para la carga inicial.
* Se corrigió el error en la configuración global.

## <a name="march-2016"></a>2016 de marzo

La versión de vista previa de marzo de 2016 de SSMA para Sybase agrega compatibilidad para la migración a SQL Server 2016.  
  
## <a name="january-2016"></a>2016 de enero

La versión de mantenimiento de enero de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
* Se ha agregado el elemento de menú Ver registro a SSMA (RFC 5706203).  
* Telemetría agregada.

## <a name="july-2014"></a>2014 de julio

La versión 2014 de julio de SSMA para Sybase contiene los siguientes cambios:  
  
* Conversión de código de Azure SQL DB mejorada.  
* Se ha cambiado la funcionalidad del paquete de extensiones al esquema para admitir Azure SQL DB.  
* Se han realizado mejoras en el rendimiento de las bases de datos con más de 10 000 objetos.  
* Se han agregado mejoras de la interfaz de usuario para tratar con un gran número de objetos.  
* Se ha agregado la capacidad de resaltar esquemas LOB "conocidos" (por lo que se pueden omitir en la conversión).  
* Mejoras en la velocidad de conversión agregada.  
* Se ha agregado la capacidad de mostrar recuentos de objetos en la interfaz de usuario.
* Menor tamaño de informe en más del 25%.  
* Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>2014 de abril

La versión de abril de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
* Compatibilidad agregada de MS SQL Server 2014.  
* Se corrigieron los errores relacionados con la conversión a Azure.  
* Se han corregido errores relacionados con las páginas del informe invisibles en IE 10.  
  
## <a name="january-2012"></a>2012 de enero

La versión 2012 de enero de SSMA para Sybase contiene los siguientes cambios:  
  
* Compatibilidad agregada para la conversión del desencadenador de reversión.
* Se proporcionó una corrección@ROWCOUNT para convertir@ERROR @ y @ en la misma instrucción set.  
  
## <a name="july-2011"></a>2011 de julio

La versión 2011 de julio de SSMA para Sybase proporciona informes de errores mejorados durante la migración de datos.  
  
## <a name="april-2011"></a>2011 de abril

La versión de abril de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
* Producto "SSMA for Sybase" consolidado, que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite 2005 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , "Denali" y Azure SQL.  
* Se ha agregado compatibilidad para conectar y migrar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Se ha agregado una nueva característica para convertir y migrar bases de datos de Sybase a Azure SQL.  
* Motor de migración de datos del lado cliente mejorado, que admite la migración en paralelo de datos.  
* Rendimiento mejorado de la migración de datos con modelos de recuperación simples y de registro masivo.
* Se ha agregado la capacidad de convertir y migrar bases de datos de Sybase que distinguen mayúsculas de minúsculas a SQL Server que distinguen mayúsculas de minúsculas.  
* Se ha agregado compatibilidad para la conversión de instrucciones de combinación no ANSI ASE de Sybase en SQL Server instrucciones de combinación ANSI se ha ampliado para eliminar y actualizar instrucciones.  
* Se proporcionan opciones de conectividad adicionales para conectarse a servidores de Sybase ASE mediante el proveedor ODBC de Sybase ASE y proveedores ADO.Net de Sybase ASE.
* Se ha quitado la dependencia de una base de datos independiente denominada **SysDB**, que contiene las funciones de emulación de Sybase (instaladas como parte del paquete de extensión).
* Se ha agregado la posibilidad de instalar SSMA para Sybase Extension [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Pack en los clústeres.
* Compatibilidad con versiones anteriores de los proyectos creados con versiones anteriores de SSMA (v 4.0 y v 4.2).  
* Se ha agregado la capacidad de instalar el producto SSMA para Sybase v 5.0 (SxS) con versiones anteriores de SSMA (v 4.0 y v 4.2).  
  
## <a name="july-2010"></a>2010 de julio

Se ha agregado la versión 2010 de julio de SSMA para Sybase:

* Compatibilidad para migrar a SQL Server 2008 R2.  
* Una nueva aplicación de consola SSMA para la ejecución de la línea de comandos.  
* Compatibilidad con la migración de datos mediante motores de migración de datos del lado cliente y del lado servidor.  
* Compatibilidad con la instrucción SELECT personalizada en la migración de datos.  
* Compatibilidad con la migración desde Sybase ASE 15.0.3 y 15,5.  
  
## <a name="june-2008"></a>2008 de junio

La versión 2008 de junio de SSMA para Sybase contiene los siguientes cambios:  
  
* Se ha agregado el comprobador de SSMA, que prueba automáticamente la conversión de objetos de base de datos y la migración de datos realizada por SSMA. Una vez finalizados todos los pasos de migración de SSMA, utilice SSMA Tester para comprobar que los objetos convertidos funcionan de la misma manera y que todos los datos se transfirieron correctamente.
* Conversión anterior a SQL agregada. Ahora, el usuario puede especificar declaraciones de tabla temporal (y de otro objeto) para cada procedimiento de origen que se va a utilizar en la conversión.
* Mejoras agregadas en la conversión de objetos:  
  * Se ha revisado la conversión.  
  * Agregados y no agregados sin cláusulas/Group by.  
  * La función IDENTITY con una instrucción SELECT INTO.  
  * Restricciones y índices en clúster en solo datos bloqueados.  
  * Tablas temporales creadas por SELECT INTO.  
  * Restricciones o índices para las tablas temporales.  
  * Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten los nuevos tipos de fecha y hora 2008.  
  * Compatibilidad con los tipos de conexión y la conectividad de Sybase 15,0.  
  
## <a name="may-2007"></a>2007 de mayo

Puede Agregar la versión 2007 de SSMA para Sybase:  
  
* La capacidad de cargar el contenido de la base de datos más rápido al guardar un proyecto.  
* Compatibilidad con comentarios introducidos por el usuario en el modo SQL con formato SQL Server.  
* Mejoras en la conversión de objetos.  

## <a name="november-2006"></a>2006 de noviembre

La versión de noviembre de 2006 de SSMA para Sybase contiene los siguientes cambios:  
  
* Nueva configuración global agregada:  
  * Puede optar por mostrar los números de línea en las ventanas del editor.  
  * Puede configurar SSMA para que solicite reemplazar objetos duplicados, o siempre o nunca reemplazar objetos duplicados durante la conversión del esquema.  
* Se ha agregado una nueva opción de conversión que le permite configurar cómo SSMA controla las situaciones siguientes:  
  * Una instrucción CAST o CONVERT que contiene una cadena binaria.  
  * Comprueba si hay valores NULL en expresiones de igualdad.  
  * Tablas de proxy.  
  * Números de error de mensaje de usuario para RAISERROR.  
  * Instrucciones UPDATE que contienen identificadores sin resolver.  
* Se ha agregado una nueva opción de migración que le permite especificar cómo SSMA debe controlar las fechas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están fuera del intervalo de fechas.  
* Se ha agregado una configuración de **SQL con formato** en la pestaña **SQL** , que da formato al código para mejorar la legibilidad.  
* Correcciones de errores, incluidos:
  * SSMA Now convierte la *tabla* de la tabla de bloqueo en {Shared | Las instrucciones de modo EXCLUSIVe} agregando una sugerencia TABLOCK o TABLOCKX a la consulta SELECT posterior de la tabla.  
  * Ahora se agregan las conversiones necesarias cuando se usan tipos binarios en expresiones de caracteres.  
  * Mejoras en la memoria y el rendimiento.  
  
## <a name="july-2006"></a>2006 de julio

La versión de julio de 2006 de SSMA para Sybase fue la versión inicial.  
  
## <a name="see-also"></a>Vea también

[Introducción con SSMA para Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)
