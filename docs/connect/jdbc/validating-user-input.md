---
title: Validando datos proporcionados por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2d890c4471dfeb85c1dd4f8f6f614a3b28cff90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003898"
---
# <a name="validating-user-input"></a>Validar los datos introducidos por el usuario

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Cuando construya una aplicación que tiene acceso a datos, debería suponer que todos los datos proporcionados por el usuario son malintencionados hasta que se demuestre lo contrario. Si no lo hace, la aplicación puede quedar en una situación de vulnerabilidad frente a ataques. Un tipo de ataque que puede producirse se denomina inyección de SQL y consiste en que se agrega código malintencionado a cadenas que luego se pasan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para analizarse y ejecutarse. Para evitar este tipo de ataque, debería utilizar procedimientos almacenados con parámetros cuando sea posible y validar siempre los datos que proporcione el usuario.

Validar los datos que proporciona el usuario en el código cliente es importante para no malgastar viajes de ida y vuelta al servidor. Es igualmente importante validar los parámetros para los procedimientos almacenados en el servidor con el fin de detectar las entradas que no son válidas y que omiten la validación del lado cliente.

Para obtener más información sobre la inyección de SQL y cómo evitarla, vea "Inyección de código SQL" en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información sobre cómo validar parámetros de procedimientos almacenados, consulte "Procedimientos almacenados ([!INCLUDE[ssDE](../../includes/ssde_md.md)])" y otros temas secundarios en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="see-also"></a>Consulte también

[Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)
