---
title: "Introducción a ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 20767544a83219c6583eaf03a78e240e15e19be2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-overview"></a>Información general ODBC
Open Database Connectivity (ODBC) es una interfaz de programación de aplicaciones ampliamente aceptada (API) para el acceso a la base de datos. Se basa en las especificaciones de la interfaz de nivel de llamada (CLI) de Open Group y ISO/IEC para las API de base de datos y usa el lenguaje de consulta estructurado (SQL) como su lenguaje de acceso de la base de datos.  
  
 ODBC está diseñado para máximo *interoperabilidad* : es decir, la capacidad de una sola aplicación para tener acceso a los sistemas de administración de otra base de datos (DBMS) con el mismo código de origen. Las aplicaciones de base de datos, llamar a funciones en la interfaz ODBC, que se implementan en módulos específicos de la base de datos denominados *controladores*. El uso de controladores aísla las aplicaciones de llamadas específicas de la base de datos de la misma manera que los controladores de impresora aislar los programas de procesamiento de texto de comandos específicos de la impresora. Dado que los controladores se cargan en tiempo de ejecución, un usuario solo tiene que agregar un nuevo controlador para tener acceso a un DBMS nueva; no es necesario volver a compilar o volver a vincular la aplicación.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Por qué se creó ODBC?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [¿Qué es ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC y la CLI estándar](../../odbc/reference/odbc-and-the-standard-cli.md)

