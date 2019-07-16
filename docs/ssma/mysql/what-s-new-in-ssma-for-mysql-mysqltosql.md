---
title: Novedades de SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 06/11/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: e3cccabc3558da3534384dacfc77e42b8d078574
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927752"
---
# <a name="whats-new-in-ssma-for-mysql-mysqltosql"></a>Novedades de SSMA para MySQL (MySQLToSql)

Este artículo se enumeran los cambios de MySQL en cada versión de SQL Server Migration Assistant (SSMA).

## <a name="ssma-v82"></a>SSMA v8.2

La versión de v8.1 de SSMA para MySQL se ha mejorado con un conjunto de correcciones diseñado para mejorar la calidad y las métricas de conversión, así como correcciones de destino:

* Un problema con los índices no clúster deshabilitados tras la migración de datos.
* Detección de .NET Framework durante la instalación silenciosa.
* Un bloqueo intermitente que se produce cuando se descarga una nueva versión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.1 a v8.2. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

> [!IMPORTANT]
> Con SSMA v7.4 y versiones posteriores, .net 4.5.2 es un requisito previo de instalación.

## <a name="ssma-v81"></a>V8.1 SSMA

La versión de v8.1 de SSMA para MySQL se ha mejorado con correcciones de destino que están diseñadas para mejorar las métricas de calidad y la conversión.

> [!NOTE]
> Un problema conocido con la actualización automática puede producir el error de una actualización desde SSMA v8.0 a v8.1. Si se produce este error, descargue la nueva versión e instalarlo manualmente.

## <a name="ssma-v80"></a>SSMA v8.0

La versión v8.0 de SSMA para MySQL se ha mejorado con correcciones de destino diseñadas para mejorar la calidad y la conversión de las métricas. Esta versión también ofrece las siguientes características nuevas:

* Compatibilidad con **Azure SQL Database Managed Instance** como destino. Ahora puede crear nuevos proyectos destinados a la instancia administrada de Azure SQL Database:

  ![Proyecto de base de datos de SQL para MI](../media/ssma-newproject-sqldbmi.png)

* Después de la conversión **corrección advisor**. Más información sobre él [aquí](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/).

* Selección de base de datos/esquema preliminar.

  Al conectarse al origen, el usuario ahora puede seleccionar las bases de datos y esquemas de interés. Seleccionar sólo los esquemas que se va a migrar ahorrará tiempo durante la conexión inicial y mejorar el rendimiento general de SSMA.

  ![Objetos de filtro SSMA](../media/ssma-filter-objects.png)

## <a name="ssma-v710"></a>SSMA v7.10

La versión de v7.10 de SSMA para MySQL contiene los siguientes cambios:

* Diseñado para proporcionar seguridad adicional y protecciones de seguridad para satisfacer los cambios en los requisitos globales correcciones de destino.
* Corrección de conversión de los espacios entre la lista de argumentos y el nombre de función.

## <a name="ssma-v79"></a>SSMA v7.9

La versión de v7.9 de SSMA para MySQL contiene los siguientes cambios:

* Correcciones de destino que mejoran las métricas de calidad y la conversión.
* Compatibilidad parcial con tipos de datos espaciales migración desde MySQL a Azure SQL Database.
* Soporte técnico en línea de comandos SSMA para modificar la asignación de tipos de datos y las preferencias del proyecto.
* Soporte técnico para migrar datos mediante SQL Server Integration Services (SSIS). Después de convertir el esquema, es posible crear un paquete SSIS mediante una opción del menú contextual.
* El cuadro de diálogo de conexión de Azure SQL Database de SSMA también se ha modificado para especificar el nombre completo del servidor. En versiones anteriores de SSMA, el prefijo de la base de datos de SQL Azure se tenía que se menciona explícitamente dentro de la configuración de proyectos.

## <a name="ssma-v78"></a>SSMA v7.8

La versión de v7.8 de SSMA para MySQL contiene los siguientes cambios:

* Cambiar la asignación de tipos de resaltado en la configuración del proyecto.
* La capacidad de los usuarios deshabilitar la telemetría.

## <a name="ssma-v77"></a>SSMA v7.7

La versión de v7.7 de SSMA para MySQL contiene los siguientes cambios:

* SSMA para MySQL se ha mejorado con correcciones de destino que mejoran las métricas de calidad y la conversión.
* Según la demanda popular, es volver la versión de 32 bits de SSMA para MySQL. En comparación con la implementación anterior (antes v7.4), hay dos paquetes de instalador, pero no se puede instalar en paralelo. Como resultado, debe elegir la versión más adecuada en función de los componentes de conectividad que tiene. Siempre es preferible usar la versión de 64 bits, si es posible.
* SSMA para MySQL ahora tiene el modo de conexión de la cadena de conexión ODBC, que le permite usar los controladores ODBC de terceros que son compatibles con MySQL.

## <a name="ssma-v76"></a>SSMA v7.6

Se ha mejorado la versión de v7.6 de SSMA para MySQL con correcciones de destino que mejoran la calidad y la conversión de las métricas y con compatibilidad con SQL Server 2017 (versión preliminar pública). Compatibilidad con SQL Server 2017 en Windows y Linux en versión preliminar pública y no debe usarse para las migraciones de producción.

## <a name="ssma-v75"></a>SSMA v7.5

La versión 7.5 de SSMA para MySQL se ha mejorado con varias mejoras para garantizar mayor accesibilidad para personas con discapacidades.

## <a name="ssma-v74"></a>SSMA v7.4

La versión v7.4 de SSMA para MySQL contiene los siguientes cambios:

* El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema de origen y destino.

    ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)
* La métrica de calidad y la conversión se ha mejorado con correcciones de destino, según los comentarios recibidos.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA está en desuso.

## <a name="ssma-v73"></a>SSMA v7.3

La versión v7.3 de SSMA para MySQL contiene los siguientes cambios:

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

La versión de v7.2 de SSMA para MySQL contiene los siguientes cambios:

* Métrica de calidad y la conversión mejorada con correcciones de destino según los comentarios recibidos.
* Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1

La versión 7.1 de SSMA para MySQL contiene los siguientes cambios:

* SQL Server 2017 en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y esquema para servidores SQL Server de destino.
* SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA en cuanto está disponible.
* Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para MySQL contiene los siguientes cambios:

* Se agregó compatibilidad para SQL Server 2016.
* Analizador mejorada y la resolución.
* Quitar la comprobación de instalador para .net 2.0.
* Dependencia del módulo de extensión actualizado de .net 3.5 a .net 4.0.
* Asignación de tipo de valor predeterminado fijo BigInt para MySql.
* Se ha corregido "guardar el proyecto" y "open project" comandos para la consola SSMA.
* Se ha corregido el comando "securepassword" para la consola SSMA.
* Se ha corregido el recuento de objetos para la carga inicial.
* Cargando los objetos MsSql fijos.
* Se corrigió el error en la configuración global.

## <a name="march-2016"></a>Marzo de 2016

La versión de vista previa de marzo de 2016 de SSMA para MySQL agrega compatibilidad para la migración a SQL Server 2016. 
  
## <a name="january-2016"></a>Enero de 2016

La versión de mantenimiento de enero de 2016 de SSMA para MySQL contiene los siguientes cambios:  

* La vista se ha agregado el elemento de menú de registro para SSMA (RFC 5706203).  
* Se ha agregado telemetría.  
  
## <a name="july-2014"></a>Julio de 2014

La versión de julio de 2014 de SSMA para MySQL contiene los siguientes cambios:  
  
* Conversión de código de Azure SQL DB mejorada. 
* Funcionalidad del módulo de extensión se mueve al esquema para admitir la base de datos de SQL Azure.  
* Mejoras de rendimiento habían probado para bases de datos con más de 10k objetos.  
* Mejoras de la interfaz de usuario para tratar con un gran número de objetos.  
* Resaltado de esquemas LOB "conocidos" (por lo que se pueden omitir en la conversión).  
* Mejoras de velocidad de conversión.  
* Mostrar recuentos de objetos en la interfaz de usuario.  
* Reducción del tamaño de informes en más del 25%.  
* Mensajes de error mejorados para construcciones sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014

La versión de abril de 2014 de SSMA para MySQL contiene los siguientes cambios:  
  
* Se agregó compatibilidad de MS SQL Server 2014.  
* Errores corregidos con respecto a la conversión a Azure  
* Errores corregidos con respecto a las páginas de informe invisible en Internet Explorer 10.  
  
## <a name="july-2011"></a>Julio de 2011

La versión de julio de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
* Admite la conversión del límite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desplazamiento "Denali".  
* Durante la migración de datos de informes de errores mejorado.  
  
## <a name="april-2011"></a>Abril de 2011

La versión de abril de 2011 de SSMA para MySQL contiene los siguientes cambios:  
  
* Solo puede instalar "SSMA para MySQL", que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" y SQL Azure.  
* La posibilidad de conectar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali".  
* Motor de migración mejorada de los datos del lado cliente, que admiten la migración paralela de datos.  
* Rendimiento de la migración de datos mejorada con Simple y masiva registra los modelos de recuperación.  
* SSMA para la versión de la consola de MySQL es compatible con la compatibilidad con versiones anteriores. Puede abrir los proyectos creados con versiones anteriores a v5.0 SSMA.  
* SSMA para MySQL v5.0 producto puede ser instalado en paralelo (SxS) con versiones anteriores del producto SSMA.  
  
## <a name="july-2010"></a>Julio de 2010

La versión de julio de 2010 de SSMA para MySQL contiene las siguientes características:  
  
1. **Mejoras en la interfaz de usuario:**  
  
    * Pestaña "Modos de SQL" para los objetos de base de datos MySQL  
    * Pestaña "Configuración" para los objetos de base de datos MySQL  
    * Pestaña 'Data' para las tablas de MySQL  
    * Configuración del proyecto actualizado en la conversión y las páginas de la migración  
    * "Configuración de migración de datos" en el nivel de tabla  
  
2. **Mejoras para conectarse a MySQL y SQL Server:**  
  
    * Conectividad SSL en MySQL  
    * Conexión cifrada en SQL Server  
  
3. **Mejoras en el Explorador de la Metabase de MySQL:**  
  
    * Carga de todos los objetos de base de datos MySQL y sus respectivas fichas.  
  
4. **Mejoras para la conversión de objeto:**
  
    * Conversión de objetos de la MySQL Metabase - procedimientos, funciones, vistas, desencadenadores y las instrucciones.  
    * Compatibilidad limitada para los tipos de datos espaciales en las tablas.
    * Opción para convertir las funciones de MySQL a procedimientos almacenados de SQL Server  
    * Opción para aplicar la asignación de juego de caracteres y modos de SQL durante la conversión de objeto  
  
5. **Mejoras en la migración de datos:**  
  
    * Compatibilidad con la migración de datos mediante motores de migración de datos del lado cliente y servidor  
    * Compatibilidad con la migración de datos espaciales  
    * SQL personalizado para la migración de datos para las tablas  
  
6. **SSMA para la consola de MySQL:**  
  
    * Compatibilidad con característica de consola de SSMA para MySQL  
    * Compatibilidad con interfaz a nivel de secuencia de comandos  
  
## <a name="january-2010"></a>Enero de 2010

La versión de enero de 2010 de SSMA para MySQL fue la versión inicial. Incluyen las siguientes características: 
  
* Se ha agregado compatibilidad para la migración a ambos local SQL Server y SQL Azure.  
  
* **Característica de instantánea:** Migración de esquema y los datos de MySQL tablas/índices y restricciones.
