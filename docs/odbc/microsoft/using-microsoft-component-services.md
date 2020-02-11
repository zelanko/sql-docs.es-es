---
title: Usar servicios de componentes de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088150"
---
# <a name="using-microsoft-component-services"></a>Uso de servicios de componentes de Microsoft
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Puede habilitar una base de datos de Oracle para que funcione con servicios de componentes transaccionales (o MTS, si usa Windows NT) en Microsoft Windows NT/Windows 2000 y Microsoft Windows 95/98. Para habilitar una base de datos de Oracle para que funcione con servicios de componentes que admiten transacciones, los administradores del sistema deben crear una vista denominada V $ XATRANS $. Para crear este script, debe ejecutar un script proporcionado por Oracle. Para obtener más información, vea la ayuda de servicios de componentes o la documentación de Oracle.
