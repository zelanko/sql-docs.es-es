---
title: La biblioteca de cursores ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbe54f6ba699bda96ce5a5ebb80a3d0988a41726
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="the-odbc-cursor-library"></a>La biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Bloque y los cursores desplazables son adiciones muy útiles para muchas aplicaciones. Sin embargo, no todos los controladores admiten bloque y los cursores desplazables. El mismo puede decirse de actualización posicionada e instrucciones delete y **SQLSetPos**, que se trata de actualizar los datos. Por lo tanto, el componente ODBC del SDK de Windows, anteriormente incluida en Microsoft Data Access Components (MDAC) SDK, incluye una biblioteca de cursores. La biblioteca de cursores implementa bloque, los cursores estáticos, actualización por posición y las instrucciones delete, y **SQLSetPos** para cualquier controlador que cumple el nivel de conformidad abierto CLI estándar de grupo. La biblioteca de cursores que se puede redistribuir con las aplicaciones ODBC; consulte el contrato de licencia en el SDK para obtener más información.  
  
 Para usar la biblioteca de cursores, una aplicación establece el atributo de conexión SQL_ATTR_ODBC_CURSORS antes de conectarse al origen de datos. Para obtener más información acerca de la biblioteca de cursores, vea [biblioteca de cursores ODBC Apéndice F:](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md).
