---
title: Controladores de Unicode | Documentos de Microsoft
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
- Unicode [ODBC], drivers
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: 3b4742d5-74fb-4aff-aa21-d83a0064d73d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26e96eaf558b82c780cba9f74c6f8636a7ab7ac7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-drivers"></a>Controladores de Unicode
Si un controlador debe ser un controlador de Unicode o ANSI depende por completo la naturaleza del origen de datos. Si el origen de datos es compatible con datos Unicode, el controlador debe ser un controlador de Unicode. Si el origen de datos solo admite datos ANSI, el controlador debe permanecer un controlador de ANSI.  
  
 Debe exportar un controlador de Unicode **SQLConnectW** se reconozca como un controlador de Unicode mediante el Administrador de controladores.  
  
 Un controlador de Unicode debe aceptar las funciones Unicode (con un sufijo de *W*) y almacenar los datos Unicode. También puede aceptar las funciones de ANSI, pero no es necesario. (El Administrador de controladores no supera una llamada de función ANSI con el *A* sufijo para el controlador, pero se convierte a un ANSI función llamada sin el sufijo y, a continuación, pasa al controlador.)  
  
 Un controlador de Unicode debe ser capaz de devolver conjuntos de resultados en Unicode o ANSI, función de enlace de la aplicación. Si una aplicación enlaza a SQL_C_CHAR, el controlador de Unicode debe convertir los datos SQL_WCHAR a SQL_CHAR. El Administrador de controladores asignará SQL_C_WCHAR a SQL_C_CHAR para controladores de ANSI pero no hace ninguna asignación para controladores de Unicode.  
  
> [!NOTE]  
>  Al determinar el tipo de controlador, el Administrador de controladores llamará **SQLSetConnectAttr** y establezca el atributo SQL_ATTR_ANSI_APP en tiempo de conexión. Si la aplicación utiliza las API de ANSI, SQL_ATTR_ANSI_APP se establecerá en SQL_AA_TRUE y, si utiliza Unicode, se establecerá en un valor de SQL_AA_FALSE. Este atributo se utiliza para que el controlador puede mostrar un comportamiento diferente en función del tipo de aplicación. El atributo no se puede establecer directamente por la aplicación y no es compatible con **SQLGetConnectAttr**. Si un controlador presenta el mismo comportamiento para las aplicaciones ANSI y Unicode, debe devolver SQL_ERROR para este atributo. Si el controlador devuelve SQL_SUCCESS, el Administrador de controladores separará conexiones ANSI y Unicode cuando se utiliza la agrupación de conexiones.
