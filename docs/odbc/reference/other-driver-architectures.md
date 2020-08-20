---
description: Otras arquitecturas de controlador
title: Otras arquitecturas de controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44a09eb786abc9f43e25ea105e25e8fdefcdff86
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499668"
---
# <a name="other-driver-architectures"></a>Otras arquitecturas de controlador
Algunos controladores ODBC no se ajustan estrictamente a la arquitectura descrita previamente. Esto puede deberse a que los controladores realizan tareas distintas de las de un controlador ODBC tradicional o no son controladores en el sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Controlador como componente intermedio  
 El controlador ODBC puede residir entre el administrador de controladores y uno o varios controladores ODBC. Cuando el controlador de la mitad es capaz de trabajar con varios orígenes de datos, actúa como un distribuidor de llamadas ODBC (o llamadas traducidas correctamente) a otros módulos que realmente tienen acceso a los orígenes de datos. En esta arquitectura, el controlador de la mitad está tomando parte de la función de un administrador de controladores.  
  
 Otro ejemplo de este tipo de controlador es un programa espía para ODBC, que intercepta y copia las funciones ODBC que se envían entre el administrador de controladores y el controlador. Esta capa se puede usar para emular un controlador o una aplicación. En el administrador de controladores, la capa parece ser el controlador; en el controlador, la capa parece ser el administrador de controladores.  
  
## <a name="heterogeneous-join-engines"></a>Motores de combinación heterogéneos  
 Algunos controladores ODBC se basan en un motor de consultas para realizar combinaciones heterogéneas. En una arquitectura de un motor de combinación heterogéneo (vea la ilustración siguiente), el controlador aparece como un controlador en la aplicación, pero aparece en otra instancia del administrador de controladores como una aplicación. Este controlador procesa una combinación heterogénea de la aplicación mediante una llamada a instrucciones SQL independientes en los controladores para cada base de datos combinada.  
  
 ![Arquitectura de un motor de combinación heterogéneo](../../odbc/reference/media/fig3-4.gif "Fig3-4")  
  
 Esta arquitectura proporciona una interfaz común para que la aplicación tenga acceso a los datos de diferentes bases de datos. Puede usar una manera común de recuperar metadatos, como información sobre columnas especiales (identificadores de fila), y puede llamar a funciones de catálogo comunes para recuperar información del Diccionario de datos. Al llamar a la función de ODBC **SQLStatistics**, por ejemplo, la aplicación puede recuperar información sobre los índices de las tablas que se van a combinar, incluso si las tablas están en dos bases de datos independientes. El procesador de consultas no tiene que preocuparse de cómo almacenan los metadatos las bases de datos.  
  
 La aplicación también tiene acceso estándar a los tipos de datos. ODBC define los tipos de datos de SQL comunes a los que se asignan los tipos de datos específicos del DBMS. Una aplicación puede llamar a **SQLGetTypeInfo** para recuperar información acerca de los tipos de datos en distintas bases de datos.  
  
 Cuando la aplicación genera una instrucción de combinación heterogénea, el procesador de consultas de esta arquitectura analiza la instrucción SQL y, a continuación, genera instrucciones SQL independientes para cada base de datos que se va a combinar. Mediante el uso de metadatos sobre cada controlador, el procesador de consultas puede determinar la combinación más eficaz y inteligente. Por ejemplo, si la instrucción combina dos tablas en una base de datos con una tabla en otra base de datos, el procesador de consultas puede combinar las dos tablas en una base de datos antes de unir el resultado con la tabla de la otra base de datos.  
  
## <a name="odbc-on-the-server"></a>ODBC en el servidor  
 Los controladores ODBC se pueden instalar en un servidor para que las aplicaciones puedan utilizarlos en cualquiera de las series de equipos cliente. En esta arquitectura (vea la ilustración siguiente), se instalan un administrador de controladores y un solo controlador ODBC en cada cliente, y se instalan en el servidor otro administrador de controladores y una serie de controladores ODBC. Esto permite que cada cliente tenga acceso a diversos controladores usados y mantenidos en el servidor.  
  
 ![Arquitectura de controladores ODBC en un servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Una ventaja de esta arquitectura es el mantenimiento y la configuración de software eficientes. Los controladores solo deben actualizarse en un lugar: en el servidor. Mediante el uso de orígenes de datos del sistema, los orígenes de datos se pueden definir en el servidor para su uso por parte de todos los clientes. No es necesario definir los orígenes de datos en el cliente. La agrupación de conexiones se puede usar para simplificar el proceso mediante el cual los clientes se conectan a los orígenes de datos.  
  
 Normalmente, el controlador del cliente es un controlador muy pequeño que transfiere la llamada del administrador de controladores al servidor. Su superficie puede ser significativamente menor que los controladores ODBC totalmente funcionales del servidor. En esta arquitectura, los recursos de cliente se pueden liberar si el servidor tiene más potencia de computación. Además, la eficacia y la seguridad de todo el sistema se pueden mejorar mediante la instalación de los servidores de copia de seguridad y el equilibrio de carga para optimizar el uso del servidor.
