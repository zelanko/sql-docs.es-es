---
title: "Invertir una transacción (Master Data Services) | Documentos de Microsoft"
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
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2c0adfc3f27bf8767f759a67001020cbbdff9f31
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="reverse-a-transaction-master-data-services"></a>Invertir una transacción (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los administradores pueden invertir una transacción cuando sea necesario deshacer una acción. Los ejemplos de transacciones son cambios del valor de atributo, movimientos de la jerarquía o eliminaciones de miembro. Este tema se aplica solo a las transacciones de las entidades con el tipo de registro de transacciones "Attribute". Vaya a la página del explorador de entidades para ver el historial de transacciones de las entidades con el tipo de registro de transacciones "Member".  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>Para invertir una transacción  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , haga clic en **Administración de versiones**.  
  
2.  En la barra de menús, haga clic en **Transacciones**.  
  
3.  En la página **Transacciones** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Versión** , seleccione una versión.  
  
5.  Haga clic en la fila de la cuadrícula correspondiente a la transacción que desea invertir.  
  
6.  Haga clic en **Invertir transacción**.  
  
7.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. Se agrega otra transacción a la cuadrícula para registrar la transacción invertida.  
  
## <a name="see-also"></a>Vea también  
 [Transacciones &#40; Master Data Services &#41;](../master-data-services/transactions-master-data-services.md)   
 [Reactivar un miembro o recopilación &#40; Master Data Services &#41;](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
 [Historial de revisiones de miembro de reversión](../master-data-services/rollback-member-revision-history-master-data-services.md)
  
  
