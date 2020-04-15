---
title: Compatibilidad con versiones anteriores de los tipos de datos de C ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304590"
---
# <a name="backward-compatibility-of-c-data-types"></a>Compatibilidad con versiones anteriores de los tipos de datos de C
SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT se han reemplazado en ODBC por tipos firmados y sin signo: SQL_C_SSHORT y SQL_C_USHORT, SQL_C_SLONG y SQL_C_ULONG y SQL_C_STINYINT y SQL_C_UTINYINT. Un controlador ODBC *3.x* que debe funcionar con aplicaciones ODBC *2.x* debe admitir SQL_C_SHORT, SQL_C_LONG y SQL_C_TINYINT, porque cuando se llaman, el Administrador de controladores los pasa al controlador.
