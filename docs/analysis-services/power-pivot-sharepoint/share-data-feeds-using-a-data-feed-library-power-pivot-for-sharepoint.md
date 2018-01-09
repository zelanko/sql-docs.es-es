---
title: Compartir las fuentes de datos mediante una biblioteca de fuentes de datos (PowerPivot para SharePoint) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: data feeds [Analysis Services with SharePoint]
ms.assetid: 4ec98dec-0cd2-4727-bb79-5bf6f8a865d6
caps.latest.revision: "26"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3c9b2b0c9ed6a70ce6e596bd1afe8bd2b49fc3a4
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint"></a>Compartir las fuentes de distribución de datos mediante una biblioteca de fuentes de distribución de datos (Power Pivot para SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Una fuente de datos es un flujo de datos XML que se genera a partir de un servicio o aplicación que expone los datos en el formato Atom. Se usa cada vez más para transportar los datos entre las aplicaciones y a los visores del lado cliente. En una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, las fuentes de distribución de datos se usan para rellenar un origen de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] con datos de una aplicación o servicio que pueden usar Atom.  
  
 Si ya utiliza una combinación de aplicaciones que pueden usar Atom, puede que nunca necesite saber cómo se generan y usan las fuentes porque la transferencia de datos se realiza sin problemas entre las aplicaciones. Sin embargo, las organizaciones que utilizan soluciones personalizadas para publicar fuentes Atom a menudo necesitan una manera de hacer que las fuentes estén disponibles para los trabajadores de la información. Una forma de conseguirlo es crear y compartir archivos de documento de servicio de datos (.atomsvc) que proporcionan las conexiones a los orígenes en línea que producen las fuentes. Una biblioteca de propósito especial, denominada biblioteca de fuentes de distribución de datos, permite crear y compartir los documentos de servicio de datos en una aplicación web de SharePoint.  
  
 Este tema contiene las siguientes secciones:  
  
 [Requisitos previos](#prereq)  
  
 [Crear un documento de servicio de datos](#createdsdoc)  
  
 [Proteger un documento de servicio de datos](#securedsdoc)  
  
 [Modificar un documento de servicio de datos](#modifydsdoc)  
  
 [Paso siguiente: usar un documento de servicio de datos](#usedsdoc)  
  
> [!NOTE]  
>  Aunque las fuentes de distribución de datos se usan para agregar datos web a un origen de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se cree en [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], cualquier aplicación cliente que pueda leer una fuente Atom puede procesar un documento de servicio de datos.  
  
##  <a name="prereq"></a> Requisitos previos  
 Debe tener una implementación de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint que agregue el procesamiento de consultas de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una granja de SharePoint. La compatibilidad con las fuentes de distribución de datos se implementa a través del paquete de soluciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Debe tener una biblioteca de SharePoint que admita el tipo de contenido de documento de servicio de datos. Para este fin se recomienda la biblioteca de fuentes de distribución de datos predeterminada, pero puede agregar manualmente el tipo de contenido a cualquier biblioteca. Para obtener más información, vea [Crear o personalizar una biblioteca de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
 Debe tener un servicio de datos o un origen de datos en línea que proporcione datos tabulares XML en el formato Atom 1.0.  
  
 Para crear o administrar un documento de servicio de datos en una biblioteca de SharePoint, debe tener los permisos de contribución en un sitio de SharePoint.  
  
##  <a name="createdsdoc"></a> Crear un documento de servicio de datos  
 Un documento de servicio de datos es una solicitud pendiente para transmitir en secuencias los datos tras la solicitud de un origen de datos en línea o una aplicación que proporcione los datos en un formato de fuente. Al crear un documento de servicio de datos, se especifica un puntero a uno o varios servicios de datos direccionables con direcciones URL que proporcionan los datos tabulares XML en el formato sindicado de Atom.  
  
 En un único documento se pueden especificar varias fuentes de distribución de datos. Esto es útil si desea recuperar un conjunto de cargas de datos del mismo servicio, o incluso de servicios diferentes, en una única operación de importación.  
  
1.  En un sitio de SharePoint, abra la biblioteca de fuentes de distribución de datos u otra biblioteca de documentos a la que haya agregado el tipo de contenido del servicio de datos y donde lo haya configurado. Para encontrar una biblioteca de fuentes de distribución de datos que se creara previamente, haga clic en **Ver todos** en Inicio rápido.  
  
2.  En la cinta de opciones en la parte superior de la página, en Herramientas de documento, haga clic en **Documentos**.  
  
3.  Haga clic en **Nuevo documento** y, a continuación, seleccione **Documento de servicio de datos**.  
  
4.  En la página Nueva documento de servicio de datos, escriba la siguiente información:  
  
    1.  El nombre y la descripción del documento de servicio de datos. Asegúrese de proporcionar detalles suficientes para que los usuarios puedan determinar si utilizan la fuente.  
  
    2.  En Fuente de datos, escriba una dirección URL a un servicio de datos o aplicación web que proporcione los datos en el formato de Atom 1.0.  
  
         La dirección URL se debe resolver como un servicio que devuelva los datos estructurados o semiestructurados en filas y columnas. El servicio debería devolver los datos anónimamente o a través de las credenciales de seguridad del usuario actual.  
  
         La dirección URL se debe resolver como un servicio compatible con la Autenticación de Windows, la autenticación básica o el acceso anónimo. El usuario que importa la fuente especifica qué esquema utilizar. La seguridad integrada está seleccionada de forma predeterminada.  
  
         La dirección URL de una fuente de distribución de datos puede incluir parámetros. Diferentes tipos de tecnologías de servicios de datos admiten esquemas de direccionamiento URL avanzados que permiten seleccionar con precisión los datos que desea utilizar. Por ejemplo, un servicio de datos de ADO.NET proporciona los parámetros de dirección URL para especificar las entidades, asociaciones y rutas de navegación en los datos subyacentes. Al especificar una dirección URL compleja como origen de una fuente de distribución de datos, puede especificar con precisión el conjunto de datos que desea utilizar.  
  
    3.  Para la misma fuente de distribución de datos, escriba un nombre de tabla que identifique posteriormente el conjunto de datos en una aplicación cliente. En [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], cada fuente de distribución de datos que importe se coloca en su propio control de tabla en un origen de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Debe especificar el nombre de la tabla que recibe los datos importados al configurar la fuente de distribución de datos.  
  
5.  Haga clic en "Agregar otra fuente de distribución de datos" para repetir los pasos previos y especificar fuentes adicionales del mismo servicio o de un servicio diferente.  
  
     Cada documento de servicio de datos se procesa como una única operación. De forma asincrónica se generarán todas las fuentes de distribución de datos en el documento y se volverán a una aplicación cliente en la misma operación. Por esta razón, especifique solo los pares de tabla y dirección URL para las fuentes de distribución de datos que desee utilizar conjuntamente.  
  
     Dado que los esquemas de autenticación se establecen en el nivel de documento de servicio de datos, cada fuente de distribución de datos adicional debe originarse a partir del servicio o aplicación que admita el mismo esquema de autenticación que la primera fuente. Todas las fuentes dentro del mismo documento de servicio de datos se autenticarán en tiempo de ejecución bajo el mismo método.  
  
6.  Guarde el documento. El documento de servicio de datos se almacena como archivo físico (.atomsvc) en una biblioteca de contenido que se configura para este tipo de contenido.  
  
 Para utilizar el documento de servicio de datos, puede abrir un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] y elegir la opción **Desde fuente de distribución de datos** en el Asistente para importar datos. Cuando se pida, un usuario especificará la dirección URL de SharePoint correspondiente al documento de servicio de datos para iniciar una operación de importación de datos. Para más información, consulte [Uso de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="securedsdoc"></a> Proteger un documento de servicio de datos  
 En un documento de servicio de datos se heredan los permisos de la biblioteca que lo contiene. Los permisos que establezca en el elemento determinarán si un usuario puede abrir, modificar o eliminar el documento de servicio de datos.  
  
 Para utilizar un documento de servicio de datos como una importación de fuentes de distribución de datos en la aplicación cliente de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , un usuario solo necesita permisos para ver el documento. Estos permisos son suficientes para resolver la dirección URL en el asistente para la importación.  
  
 Los permisos para ver en un documento de servicio de datos solo se comprueban cuando comienza una operación de importación de la fuente de distribución de datos. Después de la importación, los permisos en el documento no se comprueban de forma continuada; las fuentes que se agregaron a un origen de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existen como datos estáticos, desconectados del documento de servicio de datos que proporcionó la información de conexión original.  
  
 De igual forma, cualquier operación de actualización de datos que programe posteriormente también excluye el documento de servicio de datos. En el momento de la importación, la información de conexión para cada fuente se copia en el origen de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para la actualización. Por tanto, los permisos en un documento de servicio de datos no se comprueban para la actualización de datos, porque nunca se hace referencia al propio documento en una operación de actualización.  
  
|Tarea|Requisitos de permisos de SharePoint|  
|----------|----------------------------------------|  
|Importar fuentes de distribución de datos a un libro habilitado para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|Ver los permisos para el documento de servicio de datos en una biblioteca.|  
|En la aplicación cliente de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , actualizar los datos que se recuperaron previamente a través de una fuente.|No aplicable. La aplicación cliente de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] utiliza la información de la conexión HTTP incrustada para conectarse directamente a los servicios de datos y aplicaciones que proporcionan la fuente. La aplicación cliente de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no utiliza el documento de servicio de datos.|  
|En una granja de servidores de SharePoint, actualice los datos como una tarea programada, sin que se requiera la entrada de datos proporcionados por el usuario.|No aplicable. El servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] utiliza la información de la conexión HTTP incrustada para conectarse directamente a los servicios de datos y aplicaciones que proporcionan la fuente. El servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no utiliza el documento de servicio de datos.|  
|Eliminar un documento de servicio de datos en una biblioteca|Permisos de contribución en la biblioteca.|  
  
##  <a name="modifydsdoc"></a> Modificar un documento de servicio de datos  
 Puede agregar, modificar o quitar entradas individuales de tablas de direcciones URL en un documento de servicio de datos. Después de guardar los cambios, los usuarios que seleccionan el documento de servicio en una nueva operación de importación obtendrán las fuentes de los datos que especificó.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que utilizaban una versión anterior del documento no se verán afectados por los cambios que realice. Esto se debe a que un documento de servicio de datos solo se lee una vez durante la operación de importación inicial. Durante la importación, la dirección URL del servicio y los nombres de tabla se copian y almacenan internamente en el libro. A continuación, estos valores internos se utilizan en las operaciones de actualización subsiguientes para actualizar los datos.  
  
 Dado que no hay ningún vínculo persistente entre un documento de servicio de datos en un sitio de SharePoint y el libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que contiene la fuente importada, modificar cualquier parte de un documento de servicio de datos no tiene ningún efecto en los libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existentes.  
  
> [!IMPORTANT]  
>  Aunque el documento de servicio de datos se lee solo una vez, para obtener las fuentes más recientes se puede tener acceso a los servicios de datos que proporcionan los datos reales a intervalos regulares. Para obtener más información sobre cómo actualizar los datos, vea [Actualización de datos PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
##  <a name="usedsdoc"></a> Paso siguiente: usar un documento de servicio de datos  
 Para utilizar un documento de servicio de datos que creó en una biblioteca de SharePoint, se utiliza la opción de importación **Desde fuentes de distribución de datos** en un origen de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener instrucciones, vea [Uso de fuentes de distribución de datos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
## <a name="see-also"></a>Vea también  
 [Fuentes de distribución de datos de PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  
