---
title: "¿Qué &#39; s de SSMA para Oracle (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 09/22/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 8c43a46a3fef09fa2c8b3510b541cd545e438313
ms.openlocfilehash: 0dfba12d3b2d06677817bb087f11cbd922ca390d
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="what39s-new-in-ssma-for-oracle-oracletosql"></a>¿Qué &#39; s de SSMA para Oracle (OracleToSQL)
Este tema enumeran SSMA para cambios de Oracle en cada versión.  

## <a name="ssma-v75"></a>SSMA 7.5
La versión 7.5 de SSMA para Oracle contiene los siguientes cambios:
- Mejorado con varias mejoras para garantizar una mayor accesibilidad para personas con discapacidades.
- Actualizado para mejorar la métrica de calidad y la conversión con correcciones de destino, como la mejora del tratamiento de tipos de datos de fecha y float durante la migración de datos, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA 7.5. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v74"></a>SSMA v7.4
La versión v7.4 de SSMA para Oracle contiene los siguientes cambios:

- SSMA para Oracle ahora es compatible con almacenamiento de datos de SQL Azure como una plataforma de destino para la migración.

    ![Ventana nuevo proyecto](../media/new-project.png)
  - Es compatible con las opciones de almacenamiento de almacén de datos tal como se muestra en la siguiente imagen:

    ![Opciones de almacenamiento para el almacenamiento de datos](../media/storage-options_red.png)
  - Admite las opciones de distribución de datos tal como se muestra en la siguiente imagen:

    ![distribución de datos para almacenamiento de datos](../media/data-distribution_red.png)

- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.

    ![opción de tiempo de espera de consulta](../media/query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

## <a name="ssma-v73"></a>SSMA v7.3
La versión v7.3 de SSMA para Oracle contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  - Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    -   Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede utilizar las secuencias de comandos de esquema para realizar cambios de esquema adicionales e implementar la base de datos.
![Guardar como comando de proyecto SSDT](../media/export-schema-scripts_red.png)
  - Bibliotecas que pueden utilizarse SSMA para realizar conversiones personalizadas.
    - Ahora puede construir código que puede controlar las conversiones de sintaxis personalizados y las conversiones que antes no estaban realizaba SSMA.
      - Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión del ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Proyecto de ejemplo para la conversión se puede descargar este [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).


## <a name="ssma-v72"></a>SSMA v7.2
La versión v7.2 de SSMA para Oracle contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.

## <a name="ssma-v71"></a>SSMA v7.1
La versión 7.1 de SSMA para Oracle contiene los siguientes cambios:
- 2017 de SQL Server en Windows y Linux CTP1 ahora es una plataforma de destino admitida para la migración. Esta característica está en versión preliminar técnica y permite el movimiento de datos y el esquema para servidores SQL Server de destino.
- SSMA ahora es compatible con las actualizaciones automáticas para descargar la versión más reciente de SSMA tan pronto como está disponible.
- Archivos binarios de instalación de SSMA ahora se entregan a través de los archivos de paquete de Windows installer (.msi).

**Recursos**

[Amplía las capacidades de SQL Server Migration Assistant conversión](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)

[Evaluar y migrar datos de plataformas de datos no sean de Microsoft para SQL Server *(con el ejemplo de Oracle)*](https://blogs.msdn.microsoft.com/datamigration/2016/11/16/sql-server-migration-assistant-how-to-assess-and-migrate-databases-from-non-microsoft-data-platforms-to-sql-server/) 

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Oracle contiene los siguientes cambios:  

-   Se agregó compatibilidad para SQL Server 2016.
-   Conversión agregada Oracle retrospectiva de tablas de almacenamiento a las tablas temporales de SQL Server.
-   Conversión de agregado de Oracle VPD directiva convertir en objetos de directiva de SQL Server (seguridad de nivel de fila para Oracle).
-   Un menor tiempo de carga inicial para Oracle.
-   Analizador mejorada y resolución.
-   Quita la comprobación de instalador para .net 2.0.
-   Dependencia del módulo de extensión actualizada desde .net 3.5 a .net 4.0.
-   Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA.
-   Se ha corregido "securepassword" comando de consola SSMA.
-   Se ha corregido el recuento de objetos para la carga inicial.
-   Se ha corregido la conversión de tipos de datos de caracteres para Oracle.
-   Ha corregido el error en configuración global.
  
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para la migración a SQL Server 2016.  
-   Se agregó compatibilidad para migrar seguridad de nivel de fila Oracle (con algunas limitaciones).  
-   Agrega compatibilidad con la migración tablas de Oracle en la memoria al almacén de columnas de SQL Server.  
  
## <a name="january-2016"></a>Enero de 2016  
Enero de 2014 versión de mantenimiento de SSMA para Oracle contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para los índices clúster.  
-   Se ha corregido consultas lentas de esquema de Oracle (RFC 5076207).  
-   Fijo conectarse a Azure desde la consola.  
-   Vista ha agregado el elemento de menú de registro para SSMA (RFC 5706203). 
-   Telemetría agregada.  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para la base de datos de SQL Azure.  
-   Funcionalidad del módulo de extensión se movió al esquema para admitir la base de datos de SQL Azure.  
-   Se agregó compatibilidad para las vistas materializadas de Oracle.  
-   Ha agregado compatibilidad con memoria de SQL Server 2014 tablas optimizadas.  
-   Mejoras de rendimiento incluyen las pruebas de bases de datos con más de 10k objetos.  
-   Mejoras de interfaz de usuario agregadas para tratar con un gran número de objetos.  
-   Agrega el resaltado de los esquemas LOB "conocidos".  
-   Incluye mejoras de velocidad de conversión.  
-   Se agregó compatibilidad para mostrar el objeto de cuenta en la interfaz de usuario.  
-   Tamaño del informe reducido por más de 25%.
-   Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Se agregó compatibilidad de MS SQL Server 2014.  
-   Se agregó compatibilidad de optimización de 12 de Oracle y la consulta.  
-   Los errores corregidos en relación con la conversión a Azure.  
-   Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Ha agregado compatibilidad para parámetros de entrada RowType y Tiporegistro su valor predeterminado es NULL.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Agrega compatibilidad para la conversión de secuencia de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] generador de secuencia de "Denali".  
-   Notificación durante la migración de datos de errores mejorada.  
-   Conversión mejorada de instrucción con palabras reservadas.  
-   Mejora la conversión implícita del valor de fecha en una función.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Producto "SSMA para Oracle" consolidado, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Agrega compatibilidad para la conexión y migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
-   Motor de migración de datos de cliente mejorado, admitir la migración de paralelo de datos.  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
-   Se agregó compatibilidad para la compatibilidad con versiones anteriores de proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
-   Agrega la capacidad para instalar SSMA para Oracle v5.0 productos en paralelo (SxS) con las versiones anteriores de SSMA (v4.0 y v4.2).  
-   Ha agregado compatibilidad para tipos definidos por el usuario (incluye subtipo, VARRAY, tabla anidada, tabla de objetos y vista de objetos) y sus usos en bloques de PL/SQL con mensajes de error especial de reporting.  

## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Se agregó compatibilidad para migrar a SQL Server 2008 R2.  
-   Agrega una nueva aplicación de consola de SSMA para la ejecución de línea de comandos.  
-   Se agregó compatibilidad para la migración de datos mediante motores de migración de datos de cliente y servidor.  
-   Se agregó compatibilidad para la instrucción de "SELECT" personalizado"en la migración de datos.  
-   Se agregó compatibilidad para migrar desde Oracle 11g R2.  
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Mejoras agregadas al informe de evaluación, incluyendo información adicional de sinónimos, origen sin procesar de los objetos se puede analizar, paneles y eliminación de logotipo de SQL Server y persistencia del diseño.  
-   Mejoras agregadas en la conversión de objetos:  
    -   Paquetes DBMS_LOB, conversión DBMS_SQL agregado.  
    -   Une conversión revisado.  
    -   Modificación de recopilaciones y los registros de conversión, ahora la conversión de registros en casos más sencillos liberados con variables independientes para cada campo.  
    -   Mejoras de implementación de registros y colecciones.  
    -   Funciones de agregación basadas en ventanas agregadas.  
    -   Agrega la cláusula de paquete acumulativo de actualizaciones o el cubo.  
    -   Se ha mejorado para NEXTVAL/CURVAL.  
    -   Las columnas de agrupación en la cláusula SET, se agregaron conjuntos de agrupamiento y el Id. de agrupación.  
    -   MERGE, instrucción agregado.  
    -   Compatibilidad con nuevos tipos de fecha y hora y conversión de registros y las colecciones como tipos de datos CLR agregados.  
-   Ha agregado nuevas características de evaluador. Tablas ahora se pueden probar como objetos mediante la herramienta de comprobación, se puede modificar un orden de llamada de varios objetos pueden someterse a prueba en caso de prueba, probar procedimientos y funciones con los registros y las colecciones como parámetros y devolver valores y las dependencias de un analizador se agregó para comprobar solo utilizan tablas de usuario.  
  
## <a name="august-2007"></a>Agosto de 2007  
La versión de agosto de 2007 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Agrega que un nuevo componente de EVALUADOR le permite crear, administrar y ejecutar casos de prueba para comprobar el código SQL convertido.  
-   Ha agregado compatibilidad para la conversión de módulos locales, las recopilaciones y subtipos de Oracle se agregaron al convertidor SQL.  
-   Agrega que una nueva característica de sincronización le permite sincronizar objetos específicos con la base de datos de SQL Server.  
-   Ha agregado nuevas opciones de conversión.  
  
## <a name="april-2007"></a>Abril de 2007  
La versión de abril de 2007 de SSMA para Oracle fue la versión inicial.
