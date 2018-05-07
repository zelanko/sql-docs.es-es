---
title: Validar la entrada del usuario | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8aa867b0-e6f0-49eb-93d3-817ae2ed8f77
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 438f65ae8ec719339297b62e9bef7c347a063a1b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="validating-user-input"></a>Validar los datos introducidos por el usuario
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando construya una aplicación que tiene acceso a datos, debería suponer que todos los datos proporcionados por el usuario son malintencionados hasta que se demuestre lo contrario. Si no lo hace, la aplicación puede quedar en una situación de vulnerabilidad frente a ataques. Un tipo de ataque que puede producirse se denomina inyección de SQL, donde se agrega código malintencionado a cadenas que posteriormente se pasan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para analizarse y ejecutarse. Para evitar este tipo de ataque, debería utilizar procedimientos almacenados con parámetros cuando sea posible y validar siempre los datos que proporcione el usuario.  
  
 Validar los datos que proporciona el usuario en el código cliente es importante para no malgastar viajes de ida y vuelta al servidor. Es igualmente importante validar los parámetros para los procedimientos almacenados en el servidor con el fin de detectar las entradas que no son válidas y que omiten la validación del lado cliente.  
  
 Para obtener más información acerca de la inyección de código SQL y cómo evitar esta situación, vea "Inyección de código SQL" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla. Para obtener más información sobre la validación de parámetros de procedimiento almacenado, vea "procedimientos almacenados ([!INCLUDE[ssDE](../../includes/ssde_md.md)])" y otros temas secundarios en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
