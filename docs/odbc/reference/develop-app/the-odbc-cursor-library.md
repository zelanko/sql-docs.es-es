---
title: La biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a896a5bb41c5530c65573fa22c418199a043f8fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114069"
---
# <a name="the-odbc-cursor-library"></a>La biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Bloque y los cursores desplazables son adiciones muy útiles para muchas aplicaciones. Sin embargo, no todos los controladores admiten bloque y los cursores desplazables. El mismo puede decirse de actualización posicionada e instrucciones delete y **SQLSetPos**, que se describen en la actualización de datos. Por lo tanto, el componente ODBC del SDK de Windows, anteriormente incluida en Microsoft Data Access Components (MDAC) SDK, incluye una biblioteca de cursores. La biblioteca de cursores implementa bloque, cursores estáticos, actualización posicionada y las instrucciones delete, y **SQLSetPos** para cualquier controlador que cumple el nivel de conformidad de Open CLI estándar de grupo. La biblioteca de cursores que se puede redistribuir con las aplicaciones ODBC; consulte el contrato de licencia en el SDK para obtener más información.  
  
 Para usar la biblioteca de cursores, una aplicación establece el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse al origen de datos. Para obtener más información acerca de la biblioteca de cursores, vea [Apéndice F: Biblioteca de cursores ODBC](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
