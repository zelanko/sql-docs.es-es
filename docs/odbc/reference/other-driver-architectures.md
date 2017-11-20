---
title: Otras arquitecturas de controlador | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0a458ba0d7e83ab4e4c56ed40c34fae54e24c1b2
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="other-driver-architectures"></a>Otras arquitecturas de controlador
Algunos controladores ODBC no cumplir estrictamente la arquitectura que se ha descrito anteriormente. Esto podría deberse a que los controladores de llevar a cabo tareas distintas de las de un controlador ODBC tradicional o no son controladores en el sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Controlador como un componente central  
 El controlador ODBC puede residir entre el Administrador de controladores y uno o varios controladores ODBC. Cuando el controlador en el medio es capaz de trabajar con varios orígenes de datos, actúa como un distribuidor de las llamadas ODBC (o traducidas correctamente las llamadas) a otros módulos que realmente tener acceso a los orígenes de datos. En esta arquitectura, el controlador en el medio está tardando en algunos de los roles de un administrador de controladores.  
  
 Otro ejemplo de este tipo de controlador es un programa spy para ODBC, que intercepta y copia las funciones ODBC que se envían entre el Administrador de controladores y el controlador. Esta capa se puede utilizar para emular un controlador o una aplicación. En el Administrador de controladores, la capa aparece como el controlador; en el controlador, la capa aparece como el Administrador de controladores.  
  
## <a name="heterogeneous-join-engines"></a>Motores de combinación heterogéneo  
 Algunos controladores ODBC se basan en un motor de consulta para combinaciones heterogéneas. En una arquitectura de un motor de combinación heterogéneo (vea la ilustración siguiente), el controlador aparece en la aplicación como un controlador pero aparece en otra instancia del Administrador de controladores como una aplicación. Este controlador procesa una combinación heterogénea de la aplicación mediante una llamada a instrucciones SQL independientes en los controladores para cada base de datos combinada.  
  
 ![Arquitectura de un motor de combinación heterogéneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Esta arquitectura proporciona una interfaz común para la aplicación tener acceso a datos de bases de datos diferentes. Se puede utilizar una forma habitual de recuperar metadatos, como información sobre columnas especiales (identificadores de fila), y pueden llamar a funciones de catálogo comunes para recuperar información del diccionario de datos. Mediante una llamada a la función ODBC **SQLStatistics**, por ejemplo, la aplicación puede recuperar información acerca de los índices en las tablas que se va a combinarse, incluso si las tablas están en dos bases de datos. El procesador de consultas no tiene que preocuparse sobre cómo las bases de datos almacenan metadatos.  
  
 La aplicación también tiene acceso estándar para tipos de datos. ODBC define los tipos de datos SQL comunes que se asignan los tipos de datos específicos del DBMS a. Una aplicación puede llamar a **SQLGetTypeInfo** para recuperar información acerca de los tipos de datos en diferentes bases de datos.  
  
 Cuando la aplicación genera una instrucción de combinación heterogéneo, el procesador de consultas en esta arquitectura analiza la instrucción SQL y, a continuación, genera instrucciones de SQL independientes para cada base de datos que combinarse. Con los metadatos acerca de cada controlador, el procesador de consultas puede determinar la combinación más eficaz, inteligente. Por ejemplo, si la instrucción combina dos tablas en una base de datos con una tabla en otra base de datos, el procesador de consultas puede combinar las dos tablas en una base de datos antes de unir el resultado con la tabla de la otra base de datos.  
  
## <a name="odbc-on-the-server"></a>ODBC en el servidor  
 Controladores ODBC pueden instalarse en un servidor para que pueden ser usados por aplicaciones en cualquiera de una serie de equipos cliente. En esta arquitectura (vea la ilustración siguiente), un administrador de controladores y un único controlador ODBC se instalan en cada cliente y otro administrador de controladores y una serie de controladores ODBC instalados en el servidor. Esto permite que cada acceso de cliente a una variedad de controladores de uso y mantenimiento en el servidor.  
  
 ![Arquitectura de controladores ODBC en un servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Una ventaja de esta arquitectura es la configuración y mantenimiento de software eficaz. Controladores sólo necesitan actualizarse en un único lugar: en el servidor. Mediante el uso de orígenes de datos del sistema, los orígenes de datos se pueden definir en el servidor para su uso por todos los clientes. No es necesario definir los orígenes de datos en el cliente. Agrupación de conexiones se puede utilizar para optimizar el proceso mediante el cual los clientes se conectan a orígenes de datos.  
  
 El controlador en el cliente suele ser un controlador muy pequeño que se transfiere la llamada del Administrador de controladores al servidor. Su superficie puede ser mucho menor que los controladores ODBC totalmente funcionales en el servidor. En esta arquitectura, se pueden liberar los recursos del cliente si el servidor tiene más capacidad de proceso. Además, se pueden mejorar la eficacia y la seguridad de todo el sistema mediante la instalación de servidores de copia de seguridad y realizar el equilibrio de carga para optimizar el uso del servidor.

