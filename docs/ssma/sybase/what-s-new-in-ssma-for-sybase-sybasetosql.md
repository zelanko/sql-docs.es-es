---
title: "¿Qué &#39; s de SSMA para Sybase (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d97e03212e6985ce9d506774bfff0aa2f4ec8d1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>¿Qué &#39; s de SSMA para Sybase (SybaseToSQL)
Este tema enumeran SSMA para Sybase cambios en cada versión.  

## <a name="may-2016"></a>Mayo de 2016  
La versión de mayo de 2016 de SSMA para Sybase contiene los siguientes cambios:  

1.  Ha agregado compatibilidad con SQL Server 2016
2.  Quita la comprobación de instalador para .net 2.0
3.  Dependencias de módulo de extensión actualizado respecto a .net 3.5 a .net 4.0
4.  Fija "guardar el proyecto" y "Abrir proyecto" comandos de consola SSMA
5.  Comando "securepassword" fijo para la consola de SSMA
6.  Corregido el recuento de objetos para la carga inicial
7.  Ha corregido el error en la configuración global

## <a name="march-2016"></a>Marzo de 2016  
La versión de vista previa de marzo de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
1.  Admite la migración a SQL Server 2016  
  
## <a name="january-2016"></a>Enero de 2016  
La versión de mantenimiento de enero de 2016 de SSMA para Sybase contiene los siguientes cambios:  
  
1.  Elemento de menú de registro de la vista agregada para SSMA (RFC 5706203)  
  
2.  Telemetría agregada  
  
## <a name="july-2014"></a>Julio de 2014  
La versión de julio de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
1.  Conversión de código de base de datos de SQL Azure mejorada  
  
2.  Funcionalidad del módulo de extensión movida al esquema para admitir la base de datos de SQL Azure  
  
3.  Mejoras de rendimiento que comprueba si hay bases de datos con más de 10k objetos  
  
4.  Mejoras de la interfaz de usuario para tratar con un gran número de objetos  
  
5.  Resaltado de esquemas LOB "conocidos" (de manera que puede hacer caso omiso de conversión)  
  
6.  Mejoras de velocidad de conversión  
  
7.  Mostrar recuentos de objetos de interfaz de usuario  
  
8.  Reducción del tamaño de informes en más del 25%  
  
9. Mensajes de error mejorados para estructuras sin analizar.  
  
## <a name="april-2014"></a>Abril de 2014  
La versión de abril de 2014 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Se agregó compatibilidad de MS SQL Server 2014.  
  
-   Los errores corregidos en relación con la conversión a Azure  
  
-   Los errores corregidos en relación con páginas de informe invisible en Internet Explorer 10.  
  
## <a name="january-2012"></a>Enero de 2012  
La versión de enero de 2012 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Admite la conversión de desencadenador de reversión.  
  
-   Proporciona corrección para convertir@ROWCOUNT y @@ERROR en la misma instrucción de conjunto.  
  
## <a name="july-2011"></a>Julio de 2011  
La versión de julio de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Notificación durante la migración de datos de errores mejorada.  
  
## <a name="april-2011"></a>Abril de 2011  
La versión de abril de 2011 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Producto "SSMA para Sybase" consolidado, que es compatible con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" y SQL Azure.  
  
-   Soporte técnico para la conexión y migración a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Nueva característica para convertir y migrar las bases de datos de Sybase a SQL Azure.  
  
-   Motor de migración de datos de lado cliente, admitir la migración de paralelo de datos ha mejorado.  
  
-   Rendimiento de la migración de datos mejorada con simples y de forma masiva registra los modelos de recuperación.  
  
-   Bases de datos de Sybase entre mayúsculas y minúsculas pueden convertirse correctamente y se migra al servidor de SQL entre mayúsculas y minúsculas.  
  
-   Admite la conversión de instrucciones de combinación no ANSI de Sybase ASE a las instrucciones de combinación ANSI de SQL Server se ha ampliado para eliminar y actualizar las instrucciones.  
  
-   Opciones de conectividad adicionales para conectarse a servidores de Sybase ASE usando el proveedor de ODBC para Sybase ASE y proveedores de Sybase ASE ADO.Net.  
  
-   Eliminación de dependencia en una base de datos independiente denominado **SysDB** que contiene las funciones de emulación de Sybase (que se instala como parte del paquete de extensión).  
  
-   SSMA para Sybase: paquete de extensión ahora se puede instalar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] clústeres.  
  
-   Compatibilidad con versiones anteriores de proyectos creados con versiones anteriores de SSMA (v4.0 y v4.2).  
  
-   SSMA para Sybase v5.0 producto puede ser instalado en paralelo (SxS) con las versiones anteriores de SSMA (v4.0 y v4.2).  
  
## <a name="july-2010"></a>Julio de 2010  
La versión de julio de 2010 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Compatibilidad con la migración a SQL Server 2008 R2  
  
-   Nueva aplicación de consola de SSMA para la ejecución de la línea de comandos  
  
-   Compatibilidad para migración de datos mediante el servidor y motores de migración de datos de lado cliente  
  
-   Compatibilidad con la instrucción de "SELECT" personalizado"en la migración de datos  
  
-   Compatibilidad con la migración de Sybase ASE 15.0.3 y 15,5  
  
## <a name="june-2008"></a>Junio de 2008  
La versión de junio de 2008 de SSMA para Sybase contiene los siguientes cambios:  
  
-   SSMA evaluador agregado, prueba automáticamente la conversión del objeto de base de datos y la migración de datos realizadas por SSMA. Después de que haya finalizado todos los pasos de migración de SSMA, use SSMA evaluador para comprobar que los objetos convertidos funcionan del mismo modo y que todos los datos se transfirió correctamente.  
  
-   Agrega la conversión anterior a SQL. Usuario ahora puede especificar las tablas temporales (y otros objetos) declaraciones para cada procedimiento de origen que se usará en la conversión.  
  
-   Mejoras en la conversión de objetos:  
  
    -   Une conversión revisado.  
  
    -   Agregados y no agregados sin necesidad de/agrupar por cláusulas.  
  
    -   La función IDENTITY con una instrucción SELECT INTO.  
  
    -   Restricciones en clúster y los índices de datos solo bloqueado.  
  
    -   Tablas temporales creadas por SELECT INTO.  
  
    -   Las restricciones o índices para las tablas temporales.  
  
    -   Nueva [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se admiten los tipos de fecha y hora de 2008.  
  
    -   Compatibilidad de conectividad y los tipos de datos de Sybase 15.0.  
  
## <a name="may-2007"></a>Mayo de 2007  
La versión de mayo de 2007 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Cuando se guarda un proyecto, cargue contenido de la base de datos es más rápido.  
  
-   Compatibilidad con el servidor SQL Server con el formato modo SQL los comentarios escritos por el usuario.  
  
-   Mejoras en la conversión de objetos.  
  
Tenga en cuenta que el archivo de ayuda no se ha actualizado para esta versión. Para obtener más información, vea la sección Notas de la documentación más adelante en este tema.  
  
## <a name="november-2006"></a>Noviembre de 2006  
La versión de noviembre de 2006 de SSMA para Sybase contiene los siguientes cambios:  
  
-   Nuevos valores globales:  
  
    -   Puede optar por mostrar números de línea en las ventanas del editor.  
  
    -   Puede configurar SSMA para preguntar si desea para reemplazar objetos duplicados o siempre o nunca reemplazar objetos duplicados durante la conversión de esquema.  
  
-   Nuevas opciones de conversión le permiten configurar la forma SSMA controla las siguientes situaciones:  
  
    -   Una instrucción CAST o CONVERT que contiene una cadena binaria  
  
    -   Comprobaciones de valores null en expresiones de igualdad  
  
    -   Tablas de proxy  
  
    -   Números de error de mensaje de usuario por RAISERROR  
  
    -   Instrucciones UPDATE que contienen identificadores sin resolver  
  
-   Una nueva opción de migración le permite especificar cómo SSMA debe controlar las fechas que están fuera de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo de fechas.  
  
-   A **SQL con el formato** en el **SQL** ficha, que da formato al código para mejorar la legibilidad.  
  
-   Correcciones de errores que incluyen lo siguiente:  
  
    -   SSMA convierte ahora el bloqueo de tabla *tabla* en {SHARED | Instrucciones de modo exclusivo} mediante la adición de una sugerencia TABLOCK o TABLOCKX para la consulta SELECT subsiguientes en la tabla.  
  
    -   Ahora se han agregado las conversiones necesarias cuando se utilizan tipos de archivo binario en expresiones de caracteres.  
  
    -   Mejoras de rendimiento y memoria.  
  
## <a name="july-2006"></a>Julio de 2006  
La versión de julio de 2006 de SSMA para Sybase fue la versión inicial.  
  
## <a name="see-also"></a>Vea también  
[Introducción a SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

