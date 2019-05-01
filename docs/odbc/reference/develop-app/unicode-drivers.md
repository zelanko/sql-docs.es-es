---
title: Controladores de Unicode | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e555ff4a3b33c4c827371dc1ad63546736d7189
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473039"
---
# <a name="unicode-drivers"></a>Controladores de Unicode
Si un controlador debe ser un controlador de Unicode o ANSI depende completamente de la naturaleza del origen de datos. Si el origen de datos es compatible con datos Unicode, el controlador debe ser un controlador de Unicode. Si el origen de datos solo admite datos ANSI, el controlador debe permanecer un controlador de ANSI.  
  
 Debe exportar un controlador de Unicode **SQLConnectW** sea reconocida como un controlador de Unicode, el Administrador de controladores.  
  
 Un controlador de Unicode debe aceptar las funciones Unicode (con un sufijo de *W*) y almacenar los datos Unicode. También puede aceptar las funciones de ANSI, pero no es necesario. (El Administrador de controladores no pasa una llamada de función ANSI con el *A* sufijo para el controlador, pero convierte a ANSI función llamada sin el sufijo y pasa entonces al controlador.)  
  
 Un controlador de Unicode debe ser capaz de devolver conjuntos de resultados en Unicode o ANSI, en función de enlace de la aplicación. Si una aplicación se enlaza a SQL_C_CHAR, el controlador de Unicode debe convertir los datos SQL_WCHAR en SQL_CHAR. El Administrador de controladores SQL_C_WCHAR se asignará a SQL_C_CHAR para controladores de ANSI, pero no realiza ninguna asignación para los controladores de Unicode.  
  
> [!NOTE]  
>  Al determinar el tipo de controlador, el Administrador de controladores llamará **SQLSetConnectAttr** y establecer el atributo SQL_ATTR_ANSI_APP en tiempo de conexión. Si la aplicación usa las API de ANSI, SQL_ATTR_ANSI_APP se establecerá en SQL_AA_TRUE y, si utiliza Unicode, se establecerá en un valor de SQL_AA_FALSE. Este atributo se utiliza para que el controlador puede presentar un comportamiento diferente según el tipo de aplicación. El atributo no se puede establecer directamente por la aplicación y no es compatible con **SQLGetConnectAttr**. Si un controlador muestra el mismo comportamiento para las aplicaciones ANSI y Unicode, debe devolver SQL_ERROR para este atributo. Si el controlador devuelve SQL_SUCCESS, el Administrador de controladores separa las conexiones de ANSI y Unicode cuando se usa la agrupación de conexiones.
