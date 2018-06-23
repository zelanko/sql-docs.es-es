---
title: Invertir una transacción (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [Master Data Services], reversing
ms.assetid: 6f7c3f07-0f64-4283-8c9c-93facd00a046
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 77475ba334744f22719828027916c3f879350241
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105390"
---
# <a name="reverse-a-transaction-master-data-services"></a>Invertir una transacción (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los administradores pueden invertir una transacción cuando sea necesario deshacer una acción. Los ejemplos de transacciones son cambios del valor de atributo, movimientos de la jerarquía o eliminaciones de miembro.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Debe disponer del permiso para tener acceso al área funcional de **Administración de versiones** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-reverse-a-transaction"></a>Para invertir una transacción  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , haga clic en **Administración de versiones**.  
  
2.  En la barra de menús, haga clic en **Transacciones**.  
  
3.  En la página **Transacciones** , en la lista **Modelo** , seleccione un modelo.  
  
4.  En la lista **Versión** , seleccione una versión.  
  
5.  Haga clic en la fila de la cuadrícula correspondiente a la transacción que desea invertir.  
  
6.  Haga clic en **Invertir transacción**.  
  
7.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**. Se agrega otra transacción a la cuadrícula para registrar la transacción invertida.  
  
## <a name="see-also"></a>Vea también  
 [Las transacciones &#40;Master Data Services&#41;](../../2014/master-data-services/transactions-master-data-services.md)   
 [Reactivar un miembro o colección &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)  
  
  