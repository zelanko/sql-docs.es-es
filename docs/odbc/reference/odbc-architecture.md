---
title: Arquitectura ODBC | Documentos de Microsoft
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
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 04e952a79e026697592f8412c48eb2e065da18df
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-architecture"></a>Arquitectura ODBC
La arquitectura ODBC tiene cuatro componentes:  
  
-   **Aplicación** realiza el procesamiento y llamadas a funciones ODBC para enviar instrucciones SQL y recuperar resultados.  
  
-   **El Administrador de controladores** carga y descarga de controladores en nombre de una aplicación. Procesos ODBC, función se llama o pasa a un controlador.  
  
-   **Controlador** función procesos ODBC llama, envía solicitudes SQL a un origen de datos específico y devuelve los resultados a la aplicación. Si es necesario, el controlador modifica la solicitud de la aplicación para que la solicitud se ajusta a la sintaxis admitida por el sistema DBMS asociado.  
  
-   **Origen de datos** consiste en los datos que el usuario desea volver a acceso y su sistema operativo asociado, DBMS, y la plataforma de red (si existe) se usa para tener acceso el DBMS.  
  
 Tenga en cuenta los siguientes puntos acerca de la arquitectura ODBC. Primero, varios controladores y orígenes de datos pueden existir, que permite que la aplicación tengan acceso simultáneamente a los datos de más de un origen de datos. En segundo lugar, se utiliza la API de ODBC en dos lugares: entre la aplicación y el Administrador de controladores y entre el Administrador de controladores y cada controlador. La interfaz entre el Administrador de controladores y los controladores se conoce a veces como el *interfaz del proveedor de servicios,* o *SPI*. Para ODBC, la programación de aplicaciones (API) de la interfaz y la interfaz del proveedor de servicio (SPI) son iguales; es decir, el Administrador de controladores y cada controlador tienen la misma interfaz para las mismas funciones.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Aplicaciones](../../odbc/reference/applications.md)  
  
-   [El Administrador de controladores](../../odbc/reference/the-driver-manager.md)  
  
-   [Controladores](../../odbc/reference/drivers.md)  
  
-   [Orígenes de datos](../../odbc/reference/data-sources.md)

