---
title: Conectar con Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- connOra
ms.assetid: 711ac7ff-5d3d-4533-80ca-d1fecdb3048f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b02eb586db5bc18ffa96c8a24037d48fbe4695a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728923"
---
# <a name="connect-to-oracle"></a>Conectar con Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La primera vez que agrega o edita las tablas usadas en la instancia CDC, se le puede solicitar la conexión a la base de datos de Oracle. Debe escribir las credenciales de un usuario de Oracle que pueda obtener acceso al esquema de las tablas que se van a capturar. Escriba lo siguiente en este cuadro de diálogo:  
  
 **Autenticación**  
  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**: seleccione esta opción para usar las credenciales del dominio de Windows actual. Solo puede usar esta opción si la base de datos de Oracle está configurada para usar la autenticación de Windows.  
  
-   **Autenticación de Oracle**: si selecciona esta opción, debe escribir el **Nombre de usuario** y la **Contraseña** para el usuario en la base de datos de Oracle a la que se está conectando.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar tablas a una instancia CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)  
  
  
