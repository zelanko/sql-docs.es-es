---
title: "Anotar una transacción (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 8a737c436fa8db5eb10224d62fc0cb05635f47fa
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="annotate-a-transaction-master-data-services"></a>Anotar una transacción (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue una anotación a una transacción si desea proporcionar más información sobre la transacción con fines históricos.  
  
> [!NOTE]  
>  Las anotaciones no se pueden eliminar.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Para agregar transacciones que creó, debe contar con el permiso para obtener acceso al área funcional de **Explorador** y tener como mínimo el permiso **Actualizar** para el objeto del modelo al que desea agregar anotaciones.  
  
-   Para agregar anotaciones a las transacciones para todos los usuarios, debe tener permiso de acceso al área funcional **Administración de versiones** y ser administrador de modelos. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-annotate-a-transaction-in-explorer"></a>Para agregar anotaciones a una transacción en el Explorador  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  En la lista **Versión** , seleccione una versión.  
  
3.  Haga clic en **Explorador**.  
  
4.  En la barra de menús, seleccione **Entidades** y haga clic en la entidad que contiene el miembro que incluye una transacción a la que desee agregar anotaciones.  
  
5.  En la cuadrícula, haga clic en la fila del miembro.  
  
6.  Haga clic en **Ver transacciones**.  
  
7.  En el cuadro de diálogo **Ver transacciones** , haga clic en la transacción a la que desea agregar anotaciones.  
  
8.  En el cuadro de la parte inferior del cuadro de diálogo, escriba su anotación.  
  
9. Haga clic en **Agregar anotación**. La anotación se muestra en el panel **Anotaciones** .  
  
### <a name="to-annotate-a-transaction-in-version-management-administrators-only"></a>Para agregar anotaciones a una transacción en Administración de versiones (solo administradores)  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , haga clic en **Administración de versiones**.  
  
2.  En la barra de menús, haga clic en **Transacciones**.  
  
3.  En el panel **Transacciones** , en la cuadrícula, haga clic en la fila de la transacción a la que desea agregar anotaciones.  
  
4.  En el panel **Anotaciones de transacción** , en el cuadro **Anotación** , escriba su anotación.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Anotaciones &#40;Master Data Services&#41;](../master-data-services/annotations-master-data-services.md)   
 [Transacciones &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
  

