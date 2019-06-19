---
title: Arquitectura de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83e35d58d180336c349e83c7991d27f7007aca4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273627"
---
# <a name="odbc-architecture"></a>Arquitectura ODBC
La arquitectura de ODBC tiene cuatro componentes:  
  
-   **Aplicación** realiza el procesamiento y llamadas a funciones ODBC para enviar instrucciones SQL y recuperar resultados.  
  
-   **Administrador de controladores** cargas y descargas de controladores en nombre de una aplicación. Procesos ODBC, función se llama o pasa a un controlador.  
  
-   **Controlador** función procesos ODBC llama, envía solicitudes SQL a un origen de datos específico y devuelve los resultados a la aplicación. Si es necesario, el controlador modifica la solicitud de la aplicación para que la solicitud se ajusta a la sintaxis compatible con el DBMS asociado.  
  
-   **Origen de datos** consiste en los datos el usuario desea tener acceso y su sistema operativo asociado, DBMS, y la plataforma de red (si existe) se usa para tener acceso a la instancia de DBMS.  
  
 Tenga en cuenta los siguientes puntos acerca de la arquitectura ODBC. Primero, varios controladores y orígenes de datos pueden existir, que permite que la aplicación tengan acceso simultáneamente a los datos de más de un origen de datos. En segundo lugar, se usa la API de ODBC en dos lugares: entre la aplicación y el Administrador de controladores y entre el Administrador de controladores y cada controlador. La interfaz entre el Administrador de controladores y los controladores a veces se conoce como el *interfaz del proveedor de servicio,* o *SPI*. Para ODBC, la programación de aplicaciones (API) de la interfaz y la interfaz de proveedor de servicios (SPI) son iguales; es decir, el Administrador de controladores y cada controlador tienen la misma interfaz para las mismas funciones.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones](../../odbc/reference/applications.md)  
  
-   [El Administrador de controladores](../../odbc/reference/the-driver-manager.md)  
  
-   [Controladores](../../odbc/reference/drivers.md)  
  
-   [Orígenes de datos](../../odbc/reference/data-sources.md)
