---
title: Otras arquitecturas de controlador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd051d018cb6f53b8c08110e26bc66910e3ca4c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63045540"
---
# <a name="other-driver-architectures"></a>Otras arquitecturas de controlador
Algunos controladores ODBC no cumplir estrictamente la arquitectura descrita anteriormente. Esto puede deberse a los controladores realizan tareas distintas de las de un controlador ODBC tradicional o no son controladores en el sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Controlador como un componente central  
 El controlador ODBC puede residir entre el Administrador de controladores y uno o varios controladores ODBC. Cuando el controlador en el medio es capaz de trabajar con varios orígenes de datos, actúa como un distribuidor de llamadas ODBC (o llamadas adecuadamente traducidas) a otros módulos que realmente tienen acceso a los orígenes de datos. En esta arquitectura, el controlador en el medio está tardando en algunos de los roles del Administrador de controladores.  
  
 Otro ejemplo de este tipo de controlador es un programa spy para ODBC, que intercepta y copia las funciones ODBC que se envían entre el Administrador de controladores y el controlador. Esta capa se puede usar para emular un controlador o una aplicación. En el Administrador de controladores, la capa aparece como el controlador; para el controlador, la capa parece ser el Administrador de controladores.  
  
## <a name="heterogeneous-join-engines"></a>Motores de combinación heterogéneo  
 Algunos controladores ODBC se basan en un motor de consultas para combinaciones heterogéneas. En una arquitectura de un motor de combinación heterogéneo (vea la ilustración siguiente), aparece el controlador a la aplicación como un controlador, pero aparece en otra instancia del Administrador de controladores como una aplicación. Este controlador procesa una combinación heterogénea de la aplicación mediante una llamada a instrucciones SQL independientes en los controladores para cada base de datos combinada.  
  
 ![Arquitectura de un motor de combinación heterogéneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Esta arquitectura proporciona una interfaz común para la aplicación tener acceso a datos desde bases de datos diferentes. Se puede utilizar una forma habitual de recuperar los metadatos, como información acerca de las columnas especiales (identificadores de fila), y pueden llamar a funciones de catálogo comunes para recuperar información del diccionario de datos. Mediante una llamada a la función ODBC **SQLStatistics**, por ejemplo, la aplicación puede recuperar información acerca de los índices en las tablas que se va a combinarse, incluso si las tablas están en dos bases de datos independientes. El procesador de consultas no tiene que preocuparse por cómo almacenan los metadatos de las bases de datos.  
  
 La aplicación también tiene acceso estándar a tipos de datos. ODBC define los tipos de datos SQL comunes que se asignan los tipos de datos específicos para DBMS a. Una aplicación puede llamar a **SQLGetTypeInfo** para recuperar información sobre los tipos de datos en diferentes bases de datos.  
  
 Cuando la aplicación genera una instrucción de combinación heterogéneo, el procesador de consultas en esta arquitectura analiza la instrucción SQL y, a continuación, genera instrucciones SQL independientes para cada base de datos que se unirán. Con los metadatos acerca de cada controlador, el procesador de consultas puede determinar la combinación inteligente y más eficaz. Por ejemplo, si la instrucción combina dos tablas en una base de datos con una tabla en otra base de datos, el procesador de consultas puede combinar las dos tablas en una base de datos antes de unir el resultado con la tabla de la otra base de datos.  
  
## <a name="odbc-on-the-server"></a>ODBC en el servidor  
 Controladores ODBC pueden instalarse en un servidor para que se pueden usar las aplicaciones en cualquier parte de una serie de equipos cliente. En esta arquitectura (consulte la ilustración siguiente), un administrador de controladores y un solo controlador ODBC se instalan en cada cliente, y otro administrador de controladores y una serie de controladores ODBC instalados en el servidor. Esto permite que cada acceso de cliente a una variedad de controladores de uso y mantenimiento en el servidor.  
  
 ![Arquitectura de controladores ODBC en un servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Una ventaja de esta arquitectura es la configuración y mantenimiento de software eficaz. Los controladores solo necesitan actualizarse en un solo lugar: en el servidor. Mediante el uso de orígenes de datos del sistema, pueden definir orígenes de datos en el servidor para su uso por todos los clientes. No es necesario definir los orígenes de datos en el cliente. Agrupación de conexiones se puede usar para simplificar el proceso por el que los clientes se conectan a orígenes de datos.  
  
 El controlador en el cliente suele ser un controlador muy pequeño que se transfiere la llamada del Administrador de controladores al servidor. Su impacto puede ser significativamente menor que los controladores ODBC completamente funcionales en el servidor. En esta arquitectura, se pueden liberar los recursos de cliente si el servidor tiene más capacidad de proceso. Además, se pueden mejorar la eficacia y la seguridad de todo el sistema mediante la instalación de servidores de copia de seguridad y realizar el equilibrio de carga para optimizar el uso del servidor.
