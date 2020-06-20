---
title: Anotar una transacción (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- annotations [Master Data Services], for transactions
ms.assetid: f5a6b2ca-56de-4e42-9da8-fba0ac3e8d92
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad76c2933cf39bf1a036995a09c3713e79f5db09
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972265"
---
# <a name="annotate-a-transaction-master-data-services"></a>Anotar una transacción (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], agregue una anotación a una transacción si desea proporcionar más información sobre la transacción con fines históricos.  
  
> [!NOTE]  
>  Las anotaciones no se pueden eliminar.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Para agregar transacciones que creó, debe contar con el permiso para obtener acceso al área funcional de **Explorador** y tener como mínimo el permiso **Actualizar** para el objeto del modelo al que desea agregar anotaciones.  
  
-   Para agregar anotaciones a las transacciones para todos los usuarios, debe tener permiso de acceso al área funcional **Administración de versiones** y ser administrador de modelos. Para obtener más información, vea [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
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
  
5.  Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Anotaciones &#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)   
 [Transacciones &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)  
  
  
