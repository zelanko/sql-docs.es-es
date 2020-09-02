---
description: ODBC test es una aplicación habilitada para ODBC que se puede utilizar para probar los controladores ODBC y el administrador de controladores ODBC.
title: Prueba de ODBC
ms.custom: ''
ms.date: 09/01/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39869fe1230be75d9a76e13b8ba3938ec31ee5ee
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288250"
---
# <a name="odbc-test"></a>Prueba de ODBC

## <a name="about"></a>Acerca de

Microsoft® ODBC test es una aplicación habilitada para ODBC que puede usar para probar los controladores ODBC y el administrador de controladores ODBC. La prueba de ODBC se incluye como parte del [Kit de desarrollo de software de Microsoft Data Access Components (MDAC) 2,8](https://www.microsoft.com/download/details.aspx?id=21995).

ODBC 3,51 incluye versiones compatibles con ANSI y Unicode de la prueba de ODBC. Los archivos correspondientes son los siguientes:

- `Odbcte32.exe` y `Gtrtst32.dll` para la versión ANSI.

- `Odbct32w.exe` y `Gtrts32w.dll` para la versión Unicode.

Para usar la prueba ODBC, debe comprender la API de ODBC, el lenguaje C y SQL. Para obtener más información acerca de la API de ODBC, vea la [Referencia del programador de ODBC](../odbc/reference/odbc-programmer-s-reference.md).

Los temas de ayuda que se incluyeron anteriormente en esta sección de la documentación se encuentran ahora en el programa de prueba de ODBC. Abra `Odbcte32.exe` o `Odbct32w.exe` , abra el menú **ayuda** y, a continuación, haga clic en **temas de ayuda**.

Tenga en cuenta que las versiones de 64 bits de estas aplicaciones, destinadas a los sistemas operativos Microsoft Windows de 64 bits, tienen los mismos nombres que las versiones de 32 bits, aunque son archivos independientes. es decir, el nombre de la versión Unicode de la versión de 64 bits de la prueba de ODBC es `odbct32w.exe` .

## <a name="open-source"></a>Código abierto

La prueba ODBC es de código abierto. Para ver el código y compilar la versión más reciente de la prueba de ODBC, vaya al [repositorio de github para la prueba de ODBC](https://github.com/microsoft/ODBCTest).
