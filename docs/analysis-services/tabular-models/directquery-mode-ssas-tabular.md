---
title: "Modo DirectQuery (SSAS tabular) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.realtime.f1"
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
caps.latest.revision: 64
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 64
---
# Modo DirectQuery (SSAS tabular)
  En este tema se describe el *modo DirectQuery* para los modelos tabulares de Analysis Services con el nivel de compatibilidad 1200. El modo DirectQuery se puede activar para modelos que diseñe en SSDT, o bien para modelos tabulares que ya se hayan implementado, puede cambiar al modo DirectQuery en SSMS. Antes de elegir el modo DirectQuery, es importante comprender las ventajas y las limitaciones.
  
##  <a name="bkmk_Benefits"></a> Ventajas
 De forma predeterminada, los modelos tabulares utilizan una caché en memoria para almacenar los datos y realizar consultas en ellos. Cuando los datos de consultas de modelos tabulares residen en memoria, incluso las consultas complejas se pueden ejecutar con increíble rapidez. Pero hay algunas limitaciones para el uso de datos en caché. Es decir, los conjuntos de datos de gran tamaño pueden superar la cantidad de memoria disponible y los requisitos de actualización de datos pueden ser difíciles (por no decir imposibles) de cumplir en una programación de procesamiento normal.  
  
 DirectQuery supera estas limitaciones a la vez que también aprovecha las características de RDBMS, que mejoran la eficacia de la ejecución de las consultas. Con DirectQuery:  
  
-   Los datos están actualizados y no existe una sobrecarga adicional de administración al no tener que mantener otra copia de los datos (en la caché en memoria). Los cambios en el origen de datos subyacente se pueden reflejar inmediatamente en las consultas realizadas en el modelo de datos.  
  
-   Los conjuntos de datos pueden superar la capacidad de memoria de un servidor de Analysis Services.  
  
-   DirectQuery puede beneficiarse de la aceleración de consultas del proveedor, como la proporcionada por los índices de columnas optimizadas de memoria xVelocity.  
  
-   La seguridad se puede exigir en la base de datos back-end con características de seguridad de nivel de fila de la base de datos (como alternativa, puede usar la seguridad de nivel de fila en el modelo a través de DAX).  
  
-   Si el modelo contiene fórmulas complejas que requieren varias consultas, Analysis Services puede realizar la optimización para asegurarse de que el plan de consulta para la consulta ejecutada en la base de datos back-end sea tan eficaz como sea posible.  
  
##  <a name="bkmk_prereq"></a>Restricciones
Los modelos tabulares en el modo DirectQuery tienen algunas restricciones. Antes de cambiar de modo, es importante determinar si las ventajas de la ejecución de consultas en el servidor back-end podrían producir una reducción de funciones.  
  
 Si cambia el modo de un modelo existente en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], el Diseñador de modelos le notificará de las características del modelo que sean incompatibles con el modo DirectQuery.  
  
 En la lista siguiente se resumen las principales limitaciones de características que es necesario tener en cuenta:  
  
|||  
|-|-|  
|**Ámbito de características**|**Restricción**|  
|**Orígenes de datos**|Los modelos DirectQuery solo pueden usar datos de una única base de datos relacional de los tipos siguientes: SQL Server, base de datos SQL de Azure, Oracle y Teradata.  Vea Orígenes de datos compatibles con DirectQuery más adelante en este artículo para obtener información sobre la versión y el proveedor.| 
|**Procedimientos almacenados de SQL**|Para modelos DirectQuery, los procedimientos almacenados no se pueden especificar en una instrucción SQL para definir tablas al usar el Asistente para importar datos. |   
|**Tablas calculadas**|Las tablas calculadas no se admiten en los modelos DirectQuery, pero las columnas calculadas, sí. Si se trata de convertir un modelo tabular que contenga una columna calculada, se producirá un error que le indicará que el modelo no puede contener los datos pegados.|  
|**Límites de consulta**|El límite de filas predeterminado es un millón de filas, que se puede aumentar si especifica **MaxIntermediateRowSize** en el archivo msmdsrv.ini. Vea [Propiedades de DAX](../../analysis-services/server-properties/dax-properties.md) para más información.
|**Fórmulas DAX**|Al realizar consultas en un modelo tabular con el modo DirectQuery, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] convierte las fórmulas DAX y las definiciones de medida en instrucciones SQL. Las fórmulas DAX que contengan elementos que no se pueden convertir a sintaxis SQL devolverán errores de validación en el modelo.<br /><br /> Esta restricción está en su mayoría limitada a determinadas funciones de DAX. En lo que respecta a las medidas, las fórmulas DAX se convierten en operaciones basadas en conjuntos en el almacén de datos relacionales. Es decir, se admiten todas las medidas creadas de forma implícita. <br /><br /> Cuando se produzca un error de validación, tendrá que volver a escribir la fórmula (cambiarla por una función distinta) o usar columnas derivadas en el origen de datos como solución alternativa.  Si en un modelo tabular se incluyen fórmulas que contienen funciones no compatibles, se informará de estas fórmulas al cambiar al modo DirectQuery en el diseñador. <br /><br />**Nota:** Algunas fórmulas del modelo pueden validarse al cambiar el modelo al modo DirectQuery, pero devolverán resultados diferentes cuando se ejecuten en la memoria caché, en comparación con el almacén de datos relacional. Esto se debe a que los cálculos en la memoria caché usan la semántica del motor de análisis en memoria, que contiene características diseñadas para emular el comportamiento de Excel, mientras que las consultas en los datos almacenados en el origen de datos relacional usan la semántica de SQL Server.<br /><br /> SQL almacenado  <br /><br /> Para más información, vea [Compatibilidad de las fórmulas DAX en el modo DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md).|  
|**Coherencia de fórmula**|En algunos casos, la misma fórmula puede devolver resultados distintos en un modelo almacenado en caché, en comparación con un modelo DirectQuery que solo use el almacén de datos relacional. Estas diferencias son consecuencia de las diferencias semánticas entre el motor de análisis en memoria y SQL Server.<br /><br /> Para consultar una lista completa de los problemas de compatibilidad, incluidas las funciones que podrían devolver resultados diferentes cuando se implementa el modelo en tiempo real, vea [Compatibilidad de las fórmulas DAX en el modo DirectQuery (SQL Server Analysis Services)](http://msdn.microsoft.com/es-es/981b6a68-434d-4db6-964e-d92f8eb3ee3e).|  
|**Limitaciones de MDX**|No hay ningún nombre de objeto relativo. Todos los nombres de objetos deben ser completos.<br /><br /> Las instrucciones MDX sin ámbito de sesión (conjuntos con nombre, miembros calculados, celdas calculadas, totales visuales, miembros predeterminados, etc.), pero puede usar construcciones de ámbito de consulta, como la cláusula 'WITH'.<br /><br /> No hay tuplas con miembros de diferentes niveles en las cláusulas de subselección de MDX.<br /><br /> No hay jerarquías definidas por el usuario.<br /><br /> No hay ninguna consulta SQL nativa (normalmente, Analysis Services admite un subconjunto de T-SQL, pero no para los modelos de DirectQuery).|  

## Orígenes de datos compatibles con DirectQuery
Los modelos tabulares de DirectQuery con un nivel de compatibilidad de 1200 son compatibles con los siguientes orígenes de datos y proveedores:

Origen de datos   |Versiones  |Proveedores
---------|---------|---------
Microsoft SQL Server    |  2008 y versiones posteriores      |       Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para cliente SQL  
Base de datos SQL de Microsoft Azure    |   Todos      |  Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para cliente SQL            
Almacenamiento de datos de Microsoft Azure SQL     |   Todos     |  Proveedor de datos de .NET Framework para SQL Client       
Microsoft SQL Analytics Platform System (APS)     |   Todos      |  Proveedor OLE DB para SQL Server, Proveedor OLE DB de SQL Server Native Client, Proveedor de datos .NET Framework para cliente SQL       
Bases de datos relacionales de Oracle     |  Oracle 9i y versiones posteriores       |  Proveedor OLE DB de Oracle       
Bases de datos relacionales de Teradata    |  Teradata V2R6 y versiones posteriores     | Proveedor de datos .NET para Teradata        

## Conectar a un origen de datos
Al diseñar un modelo DirectQuery en SSDT, conectarse a un origen de datos y seleccionar las tablas y campos que quiera incluir en el modelo es un procedimiento muy similar al que se realiza con los modelos en memoria. 

Si ya ha activado DirectQuery, pero aún no se ha conectado a un origen de datos, puede usar el Asistente para la importación de tablas para conectarse al origen de datos, seleccionar tablas y campos, especificar una consulta SQL, etc. La diferencia será que, al finalizar, en realidad no se importarán datos en la caché en memoria. 

![Importación correcta de DirectQuery](../../analysis-services/tabular-models/media/directquery-import-success.png)

Si ya ha usado el Asistente para la importación de tablas para importar datos, pero aún no ha activado el modo DirectQuery, al hacerlo, se borrará la caché en memoria.

  
## Temas adicionales en esta sección
[Habilitar el modo DirectQuery en SSDT](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[Habilitar el modo DirectQuery en SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Agregar datos de ejemplo a un modelo DirectQuery en el modo de diseño](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[Definición de particiones en los modelos DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[Probar un modelo en el modo DirectQuery](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[Compatibilidad de las fórmulas DAX en el modo DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  