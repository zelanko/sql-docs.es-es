---
title: Cambiar el orden de los atributos | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 08df7b421795ad73090fe8edfbe6657ed7ffca11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754837"
---
# <a name="change-the-order-of-attributes"></a>Cambiar el orden de los atributos

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede cambiar el orden de los atributos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-the-order-of-an-attribute"></a>Para cambiar el orden de un atributo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), seleccione la fila de la entidad para la que desea crear un atributo.  
  
4.  Haga clic en **Atributos**.  
  
5.  En la página **Administrar atributos** , realice una de las siguientes acciones.  
  
    -   Si el atributo es para miembros hoja, seleccione **Hoja** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para miembros consolidados, seleccione **Consolidado** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para colecciones, seleccione **Colección** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
6.  Seleccione la fila del atributo cuyo orden desea modificar.  
  
    > [!NOTE]  
    >  No se puede modificar el orden de los atributos Nombre o Código.  
  
7.  Haga clic en **Subir** o **Bajar**.  
  
## <a name="see-also"></a>Consulte también  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
