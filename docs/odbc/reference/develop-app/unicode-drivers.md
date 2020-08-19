---
description: Controladores de Unicode
title: Controladores Unicode | Microsoft Docs
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
ms.openlocfilehash: 1acdb0c630fe5f4b1b22f51015e7ee94e7d8a56a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424487"
---
# <a name="unicode-drivers"></a>Controladores de Unicode
El hecho de que un controlador sea un controlador Unicode o un controlador ANSI depende por completo de la naturaleza del origen de datos. Si el origen de datos admite datos Unicode, el controlador debe ser un controlador Unicode. Si el origen de datos solo admite datos ANSI, el controlador debe seguir siendo un controlador ANSI.  
  
 Un controlador Unicode debe exportar **SQLConnectW** para que el administrador de controladores lo reconozca como controlador Unicode.  
  
 Un controlador Unicode debe aceptar funciones Unicode (con un sufijo de *W*) y almacenar datos Unicode. También puede aceptar funciones ANSI, pero no es necesario. (El administrador de controladores no pasa una llamada de función ANSI con *el sufijo a* del controlador, pero lo convierte en una llamada de función ANSI sin el sufijo y, a continuación, lo pasa al controlador).  
  
 Un controlador Unicode debe ser capaz de devolver conjuntos de resultados en Unicode o ANSI, dependiendo del enlace de la aplicación. Si una aplicación se enlaza a SQL_C_CHAR, el controlador Unicode debe convertir SQL_WCHAR datos en SQL_CHAR. El administrador de controladores asignará SQL_C_WCHAR a SQL_C_CHAR para los controladores ANSI, pero no realizará ninguna asignación para los controladores Unicode.  
  
> [!NOTE]  
>  Al determinar el tipo de controlador, el administrador de controladores llamará a **SQLSetConnectAttr** y establecerá el atributo de SQL_ATTR_ANSI_APP en el momento de la conexión. Si la aplicación utiliza las API ANSI, SQL_ATTR_ANSI_APP se establecerá en SQL_AA_TRUE y, si usa Unicode, se establecerá en un valor de SQL_AA_FALSE. Este atributo se usa para que el controlador pueda presentar un comportamiento diferente en función del tipo de aplicación. La aplicación no puede establecer el atributo directamente y no es compatible con **SQLGetConnectAttr**. Si un controlador exhibe el mismo comportamiento para las aplicaciones ANSI y Unicode, debe devolver SQL_ERROR para este atributo. Si el controlador devuelve SQL_SUCCESS, el administrador de controladores separará las conexiones ANSI y Unicode cuando se use la agrupación de conexiones.
