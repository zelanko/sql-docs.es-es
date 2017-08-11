---
title: "Depuración de código de la extensión de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0b7ee42be2f3d54fc8fb19ab48b3b603e29669e2
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="debugging-data-processing-extension-code"></a>Depurar el código de extensión de procesamiento de datos
  El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proporciona varias herramientas de depuración que pueden ayudarle a analizar el código de extensión de procesamiento de datos y localizar errores en él. La herramienta más conveniente dependerá de lo que intente llevar a cabo. En este ejemplo se usa [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>Para depurar el código de extensión de procesamiento de datos  
  
1.  Inicie [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] y abra el proyecto de extensión de procesamiento de datos.  
  
2.  Genere el proyecto e implemente el ensamblado de extensión de procesamiento de datos y el archivo .pdb acompañante en el Diseñador de informes. Para obtener más información acerca de la implementación, consulte [Cómo: implementar una extensión de procesamiento de datos en el Diseñador de informes](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Abra un nuevo proyecto de informe en [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] al tiempo que deja el código de la extensión de procesamiento de datos abierto en una ventana independiente de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
4.  Navegue a la ventana de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] que contenga el proyecto de extensión de procesamiento de datos y establezca algunos puntos de interrupción en el código.  
  
5.  Con el procesamiento de datos extensión proyecto la ventana activa, haga clic en **adjuntar al proceso** en el **depurar** menú.  
  
     El **adjuntar al proceso** abre el cuadro de diálogo.  
  
6.  En la lista de procesos, seleccione el proceso devenv.exe que corresponde al proyecto de informe y haga clic en **adjuntar**.  
  
7.  Defina el origen de datos de informe utilizando el **datos de informe** ficha del proyecto de informe. Probablemente utilizará el Diseñador de consultas genérico para ejecutar una consulta con el origen de datos personalizado. De esta forma se debería invocar el depurador y ejecutar el código correspondiente a sus puntos de interrupción.  
  
8.  Recorra el código con la tecla F11. Para obtener más información sobre cómo utilizar [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] para la depuración, vea la documentación de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
