---
title: "¿Qué &#39; s de SSMA para Oracle (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 191fe2e11c43f4c190a87ee52df9ff87c259ea7d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-oracle-oracletosql"></a>¿Qué &#39; s de SSMA para Oracle (OracleToSQL)
Este tema enumeran SSMA para cambios de Oracle en cada versión.  

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Oracle contiene los siguientes cambios:  

1.  Ha agregado compatibilidad con SQL Server 2016
2.  Conversión agregado Oracle retrospectiva de tablas de almacenamiento a las tablas temporales de SQL Server
3.  Conversión agregado de Oracle VPD directiva convertir en objetos de directiva de SQL Server (seguridad de nivel de fila para Oracle)
4.  Un menor tiempo de carga inicial para Oracle
5.  Resolución y analizador mejorada
6.  Quita la comprobación de instalador para .net 2.0
7.  Dependencias de módulo de extensión actualizado respecto a .net 3.5 a .net 4.0
8.  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA
9.  Comando "securepassword" fijo para la consola de SSMA
10. Corregido el recuento de objetos para la carga inicial
11. Fija la conversión de tipos de datos de caracteres para Oracle
12. Ha corregido el error en la configuración global
  
## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Oracle contiene los siguientes cambios:  
  
1.  Admite la migración a SQL Server 2016  
  
2.  Compatibilidad para migrar seguridad de nivel de fila Oracle (con algunas limitaciones)  
  
3.  Compatibilidad para migración de tablas de Oracle en la memoria al almacén de columnas de SQL Server  
  
## <a name="january-2016"></a>Enero de 2016  
Enero de 2014 versión de mantenimiento de SSMA para Oracle contiene los siguientes cambios:  
  
1.  Se agregó compatibilidad para índices agrupados  
  
2.  Consultas fijas lenta de esquema Oracle (RFC 5076207)  
  
3.  Fijo conectarse a Azure desde la consola  
  
4.  Elemento de menú de registro de la vista agregada para SSMA (RFC 5706203)  
  
5.  Telemetría agregada  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
1.  Compatibilidad con base de datos de SQL Azure  
  
2.  Funcionalidad del módulo de extensión movida al esquema para admitir la base de datos de SQL Azure  
  
3.  Compatibilidad con vistas materializadas de Oracle  
  
4.  Tablas con optimización para la compatibilidad con memoria de SQL Server 2014  
  
5.  Mejoras de rendimiento que comprueba si hay bases de datos con más de 10k objetos  
  
6.  Mejoras de la interfaz de usuario para tratar con un gran número de objetos  
  
7.  Resaltado de esquemas LOB "conocidos"  
  
8.  Mejoras de velocidad de conversión  
  
9. Mostrar recuentos de objetos de interfaz de usuario  
  
10. Reducción del tamaño de informes en más del 25%  
  
11. Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Oracle contiene los siguientes cambios:  
  
1.  Se agregó compatibilidad de MS SQL Server 2014.  
  
2.  Se agregó compatibilidad de optimización de 12 de Oracle y la consulta.  
  
3.  Los errores corregidos en relación con la conversión a Azure.  
  
4.  Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Parámetros de entrada RowType de soporte técnico y Tiporegistro su valor predeterminado es NULL.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Admite la conversión de secuencia de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] generador de secuencia de "Denali".  
  
-   Notificación durante la migración de datos de errores mejorada.  
  
-   Conversión mejorada de instrucción con palabras reservadas.  
  
-   Mejora la conversión implícita del valor de fecha en una función.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Producto "SSMA para Oracle" consolidado, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Soporte técnico para la conexión y migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Motor de migración de datos de lado cliente, admitir la migración de paralelo de datos ha mejorado.  
  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
  
-   Compatibilidad con versiones anteriores de proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
  
-   SSMA para Oracle v5.0 producto puede ser instalado en paralelo (SxS) con las versiones anteriores de SSMA (v4.0 y v4.2).  
  
-   Compatibilidad para informes (incluye subtipo, VARRAY, tabla anidada, tabla de objetos y vista de objetos) de tipos definidos por el usuario y sus usos en bloques de PL/SQL con mensajes de error especial.  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Compatibilidad con la migración a SQL Server 2008 R2  
  
-   Nueva aplicación de consola de SSMA para la ejecución de la línea de comandos  
  
-   Compatibilidad para migración de datos mediante el servidor y motores de migración de datos de lado cliente  
  
-   Compatibilidad con la instrucción de "SELECT" personalizado"en la migración de datos  
  
-   Compatibilidad con la migración de Oracle 11g R2  
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Mejoras en el informe de evaluación se completaron. Incluye información adicional para los sinónimos, origen sin procesar de los objetos se puede analizar, paneles y eliminación de logotipo de SQL Server y persistencia del diseño.  
  
-   Mejoras en la conversión de objetos:  
  
    -   Paquetes DBMS_LOB, conversión DBMS_SQL agregado.  
  
    -   Une conversión revisado.  
  
    -   Modificación de recopilaciones y los registros de conversión, ahora la conversión de registros en casos más sencillos liberados con variables independientes para cada campo.  
  
    -   Mejoras de implementación de registros y colecciones.  
  
    -   Funciones de agregación basadas en ventanas agregadas.  
  
    -   Agrega la cláusula de paquete acumulativo de actualizaciones o el cubo.  
  
    -   Se ha mejorado para NEXTVAL/CURVAL.  
  
    -   Se han agregado las columnas de agrupación en la cláusula SET, conjuntos de agrupamiento y ID de agrupación.  
  
    -   MERGE, instrucción agregado.  
  
    -   Compatibilidad con nuevos tipos de fecha y hora y conversión de registros y las colecciones como tipos de datos CLR agregados.  
  
-   Se agregaron nuevas características del evaluador. Tablas ahora se pueden probar como objetos mediante la herramienta de comprobación, se puede modificar un orden de llamada de varios objetos pueden someterse a prueba en caso de prueba, probar procedimientos y funciones con los registros y las colecciones como parámetros y devolver valores y las dependencias de un analizador se agregó para comprobar solo utilizan tablas de usuario.  
  
## <a name="august-2007"></a>Agosto de 2007  
La versión de agosto de 2007 de SSMA para Oracle contiene los siguientes cambios:  
  
-   Un nuevo componente de EVALUADOR permite crear, administrar y ejecutar casos de prueba para comprobar el código SQL convertido.  
  
-   Conversión de módulos locales, las recopilaciones y subtipos de Oracle se agregaron al convertidor SQL.  
  
-   Una nueva característica de sincronización le permite sincronizar objetos específicos con la base de datos de SQL Server.  
  
-   Agrega nuevas opciones de conversión.  
  
## <a name="april-2007"></a>Abril de 2007  
La versión de abril de 2007 de SSMA para Oracle fue la versión inicial.  
  

