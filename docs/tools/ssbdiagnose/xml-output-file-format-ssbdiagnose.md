---
title: Formato de archivo de salida de XML (ssbdiagnose) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a6ae420f6543a4395b3a7ef0f7009e43f3657cdb
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="xml-output-file-format-ssbdiagnose"></a>Formato del archivo de salida XML (ssbdiagnose)
  La utilidad **ssbdiagnose** genera la salida en forma de archivo XML si se ejecuta con el modificador **-XML** . El archivo de salida XML incluye la información de encabezado y los errores encontrados en la configuración de [!INCLUDE[ssSB](../../includes/sssb-md.md)] o la conversación que se analizó. Si lo desea, puede escribir una aplicación para analizar o notificar los errores incluidos en el archivo. O bien, puede ver el archivo XML en un editor XML estándar, como XML Notepad.  
  
 Un archivo de resultados de **ssbdiangose** contiene un elemento raíz DiagnosticInformation con dos tipos secundarios:  
  
-   Un elemento Banner con información de encabezado.  
  
-   Un elemento Issue para cada problema notificado por **ssbdiangose**.  
  
## <a name="diagnosticinformation-root-element"></a>Elemento raíz DiagnosticInformation  
  
-   [Elemento DiagnosticInformation &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Elemento Banner  
  
-   [Elemento banner &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Elemento Issue  
  
-   [Elemento Issue &#40; ssbdiagnose &#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>Vea también  
 [Utilidad ssbdiagnose &#40; Service Broker &#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  

