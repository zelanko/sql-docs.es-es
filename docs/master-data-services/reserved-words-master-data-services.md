---
title: Palabras reservadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c33bf34a99addae8a94fb92222eb3265cc6a52a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085691"
---
# <a name="reserved-words-master-data-services"></a>Palabras reservadas (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], al crear objetos del modelo o miembros, algunas palabras no se pueden usar. Su uso puede producir errores.  
  
> [!NOTE]  
>  También debe limitar el uso de caracteres especiales (símbolos, guiones, etc.).  
  
-   [Modelos](../master-data-services/reserved-words-master-data-services.md#models)  
  
-   [Entidades](../master-data-services/reserved-words-master-data-services.md#entities)  
  
-   [Jerarquías explícitas](../master-data-services/reserved-words-master-data-services.md#exhierarchies)  
  
-   [Atributos](../master-data-services/reserved-words-master-data-services.md#attributes)  
  
-   [Miembros](../master-data-services/reserved-words-master-data-services.md#members)  
  
##  <a name="models"></a> Modelos  
 Si crea un modelo con el nombre establecido en **Name** o **Code**, no seleccione **Crear entidad con el mismo nombre que el modelo** porque **Name** o **Code** no se puede usar para el nombre de una entidad.  
  
##  <a name="entities"></a> Entidades  
 Para los nombres de entidad, no puede usar **Name** o **Code**.  
  
##  <a name="exhierarchies"></a> Jerarquías explícitas  
 Para los nombres de jerarquía explícita, no puede utilizar **Name** o **Code**.  
  
##  <a name="attributes"></a> Atributos  
  
-   **ID**  
  
-   **Code**  
  
-   **EnterUserName**  
  
-   **LastChgUserName**  
  
-   **Name**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a> Miembros  
 Para los miembros, no puede usar **MDMMemberStatus**, **MDMUnused**o **ROOT** para el valor de atributo **Code** .  
  
## <a name="see-also"></a>Vea también  
 [Introducción a Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
  
