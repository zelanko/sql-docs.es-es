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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb5763058fa198cbad7464434e31942ef8d6cd7d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307586"
---
# <a name="using-microsoft-component-services"></a>Uso de servicios de componentes de Microsoft
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Puede habilitar una base de datos de Oracle para que funcione con servicios de componentes transaccionales (o MTS, si usa Windows NT) en Microsoft Windows NT/Windows 2000 y Microsoft Windows 95/98. Para habilitar una base de datos de Oracle para que funcione con servicios de componentes que admiten transacciones, los administradores del sistema deben crear una vista denominada V $ XATRANS $. Para crear este script, debe ejecutar un script proporcionado por Oracle. Para obtener más información, vea la ayuda de servicios de componentes o la documentación de Oracle.
