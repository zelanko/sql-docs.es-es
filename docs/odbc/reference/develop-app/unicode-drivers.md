---
title: Controladores Unicode ?? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aabdd899d78c1141716725d57e343dc002dc96ad
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284357"
---
# <a name="unicode-drivers"></a>Controladores de Unicode
Si un controlador debe ser un controlador Unicode o un controlador ANSI depende totalmente de la naturaleza del origen de datos. Si el origen de datos admite datos Unicode, el controlador debe ser un controlador Unicode. Si el origen de datos solo admite datos ANSI, el controlador debe seguir siendo un controlador ANSI.  
  
 Un controlador Unicode debe exportar **SQLConnectW** para que el Administrador de controladores reconozca como controlador Unicode.  
  
 Un controlador Unicode debe aceptar funciones Unicode (con un sufijo *W*) y almacenar datos Unicode. También puede aceptar funciones ANSI, pero no es necesario. (El Administrador de controladores no pasa una llamada de función ANSI con el sufijo *A* al controlador, pero la convierte en una llamada de función ANSI sin el sufijo y, a continuación, la pasa al controlador.)  
  
 Un controlador Unicode debe ser capaz de devolver conjuntos de resultados en Unicode o ANSI, dependiendo del enlace de la aplicación. Si una aplicación se enlaza a SQL_C_CHAR, el controlador Unicode debe convertir SQL_WCHAR datos en SQL_CHAR. El administrador de controladores asignará SQL_C_WCHAR a SQL_C_CHAR para los controladores ANSI, pero no realiza ninguna asignación para los controladores Unicode.  
  
> [!NOTE]  
>  Al determinar el tipo de controlador, el Administrador de controladores llamará a **SQLSetConnectAttr** y establecerá el SQL_ATTR_ANSI_APP atributo en tiempo de conexión. Si la aplicación utiliza las API ANSI, SQL_ATTR_ANSI_APP se establecerá en SQL_AA_TRUE y, si utiliza Unicode, se establecerá en un valor de SQL_AA_FALSE. Este atributo se utiliza para que el controlador pueda mostrar un comportamiento diferente en función del tipo de aplicación. La aplicación no puede establecer el atributo directamente y **SQLGetConnectAttr**no lo admite. Si un controlador muestra el mismo comportamiento para las aplicaciones ANSI y Unicode, debe devolver SQL_ERROR para este atributo. Si el controlador devuelve SQL_SUCCESS, el Administrador de controladores separará las conexiones ANSI y Unicode cuando se utilice Agrupación de conexiones.
