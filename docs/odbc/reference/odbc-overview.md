---
title: Información general sobre ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC]
- ODBC [ODBC], about ODBC
ms.assetid: 233315bd-2b7f-4b20-9978-e920e1ea9a07
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a0515a882cd7d1c97a60e9262942bd7c397b0b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298295"
---
# <a name="odbc-overview"></a>Información general sobre ODBC
La conectividad abierta de bases de datos (ODBC) es una interfaz de programación de aplicaciones (API) ampliamente aceptada para el acceso a bases de datos. Se basa en las especificaciones de la interfaz de nivel de llamada (CLI) de Open Group e ISO/IEC para las API de base de datos y usa Lenguaje de consulta estructurado (SQL) como su lenguaje de acceso a bases de datos.  
  
 ODBC está diseñado para obtener la máxima *interoperabilidad* , es decir, la capacidad de una sola aplicación para tener acceso a diferentes sistemas de administración de bases de datos (DBMS) con el mismo código fuente. Las aplicaciones de base de datos llaman a funciones de la interfaz ODBC, que se implementan en módulos específicos de la base de datos denominados *Controladores*. El uso de controladores aísla las aplicaciones de las llamadas específicas de la base de datos de la misma manera que los controladores de impresora aíslan los programas de procesamiento de texto de los comandos específicos de la impresora. Dado que los controladores se cargan en tiempo de ejecución, un usuario solo tiene que agregar un nuevo controlador para tener acceso a un nuevo DBMS; no es necesario volver a compilar o volver a vincular la aplicación.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Por qué se creó ODBC?](../../odbc/reference/why-was-odbc-created.md)  
  
-   [¿Qué es ODBC?](../../odbc/reference/what-is-odbc.md)  
  
-   [ODBC y la CLI estándar](../../odbc/reference/odbc-and-the-standard-cli.md)
