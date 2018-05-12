---
title: Clases de OLAP en AMO | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1d457c26a0b2d33058a5eb496825a6dc03dbc71
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="amo-olap-classes"></a>Clases de OLAP en AMO
  Las clases de OLAP en AMO (Objetos de administración de análisis) sirven de ayuda para crear, modificar, eliminar y procesar cubos, dimensiones y objetos relacionados como indicadores de clave de rendimiento (KPI), acciones y almacenamiento en caché automático.  
  
 Para obtener más información acerca de cómo configurar el entorno de programación de AMO, cómo establecer una conexión con un servidor de acceso a una base de datos o definir los datos de orígenes y vistas del origen de datos, vea [clases fundamentales de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Objetos de dimensión](#Dimensions)  
  
-   [Objetos de cubo](#Cubes)  
  
-   [Objetos MeasureGroup](#MeasureGroups)  
  
-   [Objetos de partición](#Partition)  
  
-   [Objetos AggregationDesign](#AggregationDesign)  
  
-   [Objetos Aggregation](#Aggregation)  
  
-   [Objetos Action](#Action)  
  
-   [Objetos KPI](#KPI)  
  
-   [Objetos de perspectiva](#Perspective)  
  
-   [Objetos Translation](#Translation)  
  
-   [Objetos ProactiveCaching](#ProactiveCaching)  
  
 La ilustración siguiente muestra la relación de las clases que se explican en este tema.  
  
 ![Clases OLAP en AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-olapclasses.gif "clases OLAP en AMO")  
  
## <a name="basic-classes"></a>Clases básicas  
  
###  <a name="Dimensions"></a> Objetos de dimensión  
 Para crear una dimensión, ésta se agrega a la colección de dimensiones de la base de datos primaria y el objeto <xref:Microsoft.AnalysisServices.Dimension> se actualiza en el servidor mediante el método Update.  
  
 Para quitar una dimensión, ésta se quita mediante el método Drop de <xref:Microsoft.AnalysisServices.Dimension>. Cuando se quita un objeto <xref:Microsoft.AnalysisServices.Dimension> de la colección de dimensiones de la base de datos mediante el método Remove, no se elimina del servidor, únicamente se elimina en el modelo de objetos AMO.  
  
 Se puede procesar un objeto <xref:Microsoft.AnalysisServices.Dimension> una vez que se ha creado. <xref:Microsoft.AnalysisServices.Dimension> se puede procesar mediante su propio método de proceso o bien con el método de proceso del objeto primario cuando se procesa el objeto primario.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Dimension> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Cubes"></a> Objetos de cubo  
 Para crear un cubo, éste se agrega a la colección de cubos de la base de datos y el objeto <xref:Microsoft.AnalysisServices.Cube> se actualiza en el servidor mediante el método Update. El método Update del cubo puede incluir el parámetro UpdateOptions.ExpandFull, que garantiza que todos los objetos del cubo que se han modificado se actualizarán en el servidor en esta acción de actualización.  
  
 Para quitar un cubo, se tiene que hacer mediante el método Drop de <xref:Microsoft.AnalysisServices.Cube>. Quitar un cubo de la colección no afecta al servidor.  
  
 Se puede procesar un objeto <xref:Microsoft.AnalysisServices.Cube> una vez que se ha creado. <xref:Microsoft.AnalysisServices.Cube> se puede procesar mediante su propio método de proceso o bien cuando un objeto primario se procese con su propio método Process.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Cube> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="MeasureGroups"></a> Objetos MeasureGroup  
 Para crear un grupo de medida, éste se agrega a la colección de grupo de medida del cubo y el objeto <xref:Microsoft.AnalysisServices.MeasureGroup> se actualiza en el servidor mediante su propio método Update. Para quitar un objeto <xref:Microsoft.AnalysisServices.MeasureGroup>, se usa su propio método Drop.  
  
 Se puede procesar un objeto <xref:Microsoft.AnalysisServices.MeasureGroup> una vez que se ha creado. <xref:Microsoft.AnalysisServices.MeasureGroup> se puede procesar mediante su propio método Process o bien cuando un objeto primario se procese con su propio método Process.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.MeasureGroup> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Partition"></a> Objetos de partición  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Partition>, éste se agrega a la colección de particiones del grupo de medida primario y el objeto <xref:Microsoft.AnalysisServices.Partition> se actualiza en el servidor mediante el método Update. Para quitar un objeto <xref:Microsoft.AnalysisServices.Partition>, se usa el método Drop.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Partition> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="AggregationDesign"></a> Objetos AggregationDesign  
 Los diseños de agregaciones se construyen mediante el método AggregationDesign de un objeto <xref:Microsoft.AnalysisServices.AggregationDesign>.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.AggregationDesign> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Aggregation"></a> Objetos Aggregation  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Aggregation>, éste se agrega a la colección de diseños de agregaciones del grupo de medida primario y el objeto de grupo de medida primario se actualiza en el servidor mediante el método Update. Una agregación se quita de <xref:Microsoft.AnalysisServices.AggregationCollection> mediante el método Remove o el método RemoveAt.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Aggregation> en <xref:Microsoft.AnalysisServices>.  
  
## <a name="advanced-classes"></a>Clases avanzadas  
 Las clases avanzadas proporcionan funciones OLAP sin limitarse únicamente a generar y examinar un cubo. Las siguientes son algunas de las clases avanzadas y las ventajas que proporcionan:  
  
-   Las clases Action se utilizan para crear una respuesta activa al examinar ciertas áreas del cubo.  
  
-   Los indicadores clave de rendimiento (KPI) habilitan el análisis de comparación entre valores de datos.  
  
-   Las perspectivas proporcionan vistas seleccionadas de un cubo único, de manera que los usuarios se puedan centrar en lo que es importante para ellos.  
  
-   Las traducciones permiten personalizar el cubo con la configuración regional del usuario.  
  
-   Las clases de almacenamiento en caché automático proporcionan un equilibrio entre el rendimiento mejorado del almacenamiento MOLAP y la inmediatez del almacenamiento ROLAP, así como un proceso de particiones programado.  
  
 AMO se usa para establecer las definiciones de este comportamiento mejorado, pero la experiencia real la define el cliente de exploración que implementa todas estas mejoras.  
  
###  <a name="Action"></a> Objetos Action  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Action>, éste se agrega a la colección de acciones del cubo y el objeto <xref:Microsoft.AnalysisServices.Cube> se actualiza en el servidor mediante el método Update. El método Update del cubo puede incluir el parámetro UpdateOptions.ExpandFull, que garantiza que todos los objetos del cubo que se han modificado se actualizarán en el servidor con esta acción de actualización.  
  
 Para quitar un <xref:Microsoft.AnalysisServices.Action> objeto, éste se debe quitar de la colección y se debe actualizar el cubo primario.  
  
 Un cubo se debe actualizar y procesar antes de que se pueda utilizar la acción desde el cliente.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Action> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="KPI"></a> Objetos KPI  
 Para crear un objeto  <xref:Microsoft.AnalysisServices.Kpi>, éste se agrega a la colección KPI del cubo y el objeto <xref:Microsoft.AnalysisServices.Cube> se actualiza en el servidor mediante el método Update. El método Update del cubo puede incluir el parámetro UpdateOptions.ExpandFull, que garantiza que todos los objetos del cubo que se han modificado se actualizarán en el servidor con esta acción de actualización.  
  
 Para quitar un <xref:Microsoft.AnalysisServices.Kpi> objeto, éste se debe quitar de la colección, y se debe actualizar el cubo primario.  
  
 Un cubo se debe actualizar y procesar antes de que se pueda usar el KPI.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Kpi> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Perspective"></a> Objetos de perspectiva  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Perspective>, éste se debe agregar a la colección de perspectivas del cubo y el objeto <xref:Microsoft.AnalysisServices.Cube> se debe actualizar en el servidor mediante el método Update. El método Update del cubo puede incluir el parámetro UpdateOptions.ExpandFull, que garantiza que todos los objetos del cubo que se han modificado se actualizarán en el servidor con esta acción de actualización.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.Perspective>, éste se debe quitar de la colección y se debe actualizar el cubo primario  
  
 Para usar la perspectiva, el cubo debe estar actualizado y haberse procesado.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Perspective> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="Translation"></a> Objetos Translation  
 Para crear un objeto <xref:Microsoft.AnalysisServices.Translation>, éste se debe agregar a la colección de traducción del objeto deseado y el objeto principal primario más próximo se debe actualizar en el servidor mediante el método Update. El método Update del objeto primario más próximo puede incluir el parámetro UpdateOptions.ExpandFull, que garantiza que todos los objetos secundarios que se han modificado se actualizarán en el servidor con esta acción de actualización.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.Translation>, éste se debe quitar de la colección y se debe actualizar el objeto primario más próximo.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.Translation> en <xref:Microsoft.AnalysisServices>.  
  
###  <a name="ProactiveCaching"></a> Objetos ProactiveCaching  
 Para crear un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>, éste se agrega a la colección de objetos de almacenamiento en caché automático de la dimensión o partición, y el objeto de dimensión o partición se debe actualizar en el servidor mediante el método Update.  
  
 Para quitar un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>, éste se debe quitar de la colección y se debe actualizar el objeto primario  
  
 Una dimensión o partición se debe actualizar y procesar antes de que el almacenamiento en caché automático se habilite y esté listo para utilizarse.  
  
 Para obtener más información acerca de los métodos y propiedades disponibles, vea <xref:Microsoft.AnalysisServices.ProactiveCaching> en <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Programar objetos básicos OLAP de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-basic-objects.md)   
 [Objetos avanzados OLAP en AMO programación](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-olap-advanced-objects.md)   
 [Arquitectura lógica & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
