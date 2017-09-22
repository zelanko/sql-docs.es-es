---
title: Aplicar reglas de calidad de datos al origen de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: c28834d50b2b81be99c29fb97c6227380b05c5d1
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="apply-data-quality-rules-to-data-source"></a>Aplicar reglas de calidad de los datos al origen de datos
  Puede utilizar Data Quality Services (DQS) para corregir los datos en el flujo de datos de paquete conectando la transformación de Limpieza de DQS con el origen de datos. Para obtener más información acerca de DQS, vea [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md). Para obtener más información sobre la transformación, vea [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 Al procesar datos con la transformación Limpieza DQS, se crea un proyecto de calidad de datos en el servidor Data Quality Server. Utilice Data Quality Client para administrar el proyecto. Para más información, consulte [Abrir, desbloquear, cambiar nombre y eliminar un proyecto de calidad de los datos](/sql-docs/docs/data-quality-services/open-unlock-rename-and-delete-a-data-quality-project).  
  
### <a name="to-correct-data-in-the-data-flow"></a>Para corregir datos en el flujo de datos  
  
1.  Cree un paquete.  
  
2.  Agregue y configure la transformación Limpieza de DQS. Para más información, consulte [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md).  
  
3.  Conecte la transformación Limpieza de DQS a un origen de datos.  
  
  
