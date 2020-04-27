---
title: Palabras reservadas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- reserved words [Master Data Services]
- Master Data Services, reserved words
ms.assetid: 88afd0d0-4362-4394-8357-4e65388fc0fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 5435c2a48417156abd6d4f831bf61c9ba6440fab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482578"
---
# <a name="reserved-words-master-data-services"></a>Palabras reservadas (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], al crear objetos del modelo o miembros, algunas palabras no se pueden usar. Su uso puede producir errores.  
  
> [!NOTE]  
>  También debe limitar el uso de caracteres especiales (símbolos, guiones, etc.).  
  
-   [Modelos](#models)  
  
-   [Entidades](#entities)  
  
-   [Jerarquías explícitas](#exhierarchies)  
  
-   [Atributos](#attributes)  
  
-   [Members](#members)  
  
##  <a name="models"></a><a name="models"></a>Modelos  
 Si crea un modelo con el nombre establecido en **nombre**, no seleccione **crear entidad con el mismo nombre que el modelo** porque **el nombre no se puede** usar para el nombre de una entidad.  
  
##  <a name="entities"></a><a name="entities"></a>Jurídica  
 Para los nombres de entidad, no puede usar **Name** o **Code**.  
  
##  <a name="explicit-hierarchies"></a><a name="exhierarchies"></a>Jerarquías explícitas  
 Para los nombres de jerarquía explícita, no puede utilizar **Name** o **Code**.  
  
##  <a name="attributes"></a><a name="attributes"></a>Sus  
  
-   **Id**  
  
-   **Código**  
  
-   **Nombre**  
  
-   **EnterDTM**  
  
-   **EnterUserID**  
  
-   **EnterUserName**  
  
-   **LastChgDTM**  
  
-   **LastChgUserID**  
  
-   **Status_ID**  
  
-   **ValidationStatus_ID**  
  
-   **Version_ID**  
  
##  <a name="members"></a><a name="members"></a>Registrados  
 Para los miembros, no puede usar **MDMMemberStatus** o **root** para el valor del atributo **code** .  
  
## <a name="see-also"></a>Consulte también  
 [Introducción a Master Data Services](master-data-services-overview-mds.md)  
  
  
