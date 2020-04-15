---
title: Otras arquitecturas de conductores ( Microsoft Docs
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
ms.openlocfilehash: ae047fe8014b806d3bda8b0513521b4ddda072a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280535"
---
# <a name="other-driver-architectures"></a>Otras arquitecturas de controlador
Algunos controladores ODBC no se ajustan estrictamente a la arquitectura descrita anteriormente. Esto puede deberse a que los controladores realizan tareas distintas de las de un controlador ODBC tradicional o no son controladores en el sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Controlador como componente medio  
 El controlador ODBC puede residir entre el Administrador de controladores y uno o más controladores ODBC. Cuando el controlador en el medio es capaz de trabajar con varios orígenes de datos, actúa como un distribuidor de llamadas ODBC (o llamadas traducidas adecuadamente) a otros módulos que realmente tienen acceso a los orígenes de datos. En esta arquitectura, el controlador en el medio está asumiendo parte del papel de un administrador de controladores.  
  
 Otro ejemplo de este tipo de controlador es un programa espía para ODBC, que intercepta y copia las funciones ODBC que se envían entre el Administrador de controladores y el controlador. Esta capa se puede utilizar para emular un controlador o una aplicación. Para el Administrador de controladores, la capa parece ser el controlador; al controlador, la capa parece ser el Administrador de controladores.  
  
## <a name="heterogeneous-join-engines"></a>Motores de unión heterogéneos  
 Algunos controladores ODBC se basan en un motor de consultas para realizar combinaciones heterogéneas. En una arquitectura de un motor de combinación heterogéneo (consulte la siguiente ilustración), el controlador aparece en la aplicación como un controlador, pero aparece en otra instancia del Administrador de controladores como una aplicación. Este controlador procesa una combinación heterogénea desde la aplicación llamando a instrucciones SQL independientes en controladores para cada base de datos unida.  
  
 ![Arquitectura de un motor de combinación heterogéneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Esta arquitectura proporciona una interfaz común para que la aplicación acceda a los datos de diferentes bases de datos. Puede usar una forma común de recuperar metadatos, como información sobre columnas especiales (identificadores de fila) y puede llamar a funciones de catálogo comunes para recuperar información del diccionario de datos. Al llamar a la función ODBC **SQLStatistics**, por ejemplo, la aplicación puede recuperar información sobre los índices de las tablas que se van a unir, incluso si las tablas están en dos bases de datos independientes. El procesador de consultas no tiene que preocuparse por cómo las bases de datos almacenan metadatos.  
  
 La aplicación también tiene acceso estándar a los tipos de datos. ODBC define tipos de datos SQL comunes a los que se asignan tipos de datos específicos de DBMS. Una aplicación puede llamar a **SQLGetTypeInfo** para recuperar información sobre los tipos de datos en diferentes bases de datos.  
  
 Cuando la aplicación genera una instrucción join heterogénea, el procesador de consultas de esta arquitectura analiza la instrucción SQL y, a continuación, genera instrucciones SQL independientes para cada base de datos que se va a unir. Mediante el uso de metadatos sobre cada controlador, el procesador de consultas puede determinar la combinación inteligente y más eficaz. Por ejemplo, si la instrucción une dos tablas en una base de datos con una tabla en otra base de datos, el procesador de consultas puede unir las dos tablas de la base de datos antes de unir el resultado con la tabla de la otra base de datos.  
  
## <a name="odbc-on-the-server"></a>ODBC en el servidor  
 Los controladores ODBC se pueden instalar en un servidor para que puedan ser utilizados por las aplicaciones en cualquiera de una serie de equipos cliente. En esta arquitectura (consulte la siguiente ilustración), un Administrador de controladores y un único controlador ODBC se instalan en cada cliente y otro Administrador de controladores y una serie de controladores ODBC se instalan en el servidor. Esto permite a cada cliente acceder a una variedad de controladores utilizados y mantenidos en el servidor.  
  
 ![Arquitectura de controladores ODBC en un servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Una ventaja de esta arquitectura es el mantenimiento y la configuración eficientes del software. Los controladores solo necesitan actualizarse en un solo lugar: en el servidor. Mediante el uso de orígenes de datos del sistema, los orígenes de datos se pueden definir en el servidor para su uso por todos los clientes. No es necesario definir los orígenes de datos en el cliente. La agrupación de conexiones se puede utilizar para optimizar el proceso mediante el cual los clientes se conectan a orígenes de datos.  
  
 El controlador en el cliente suele ser un controlador muy pequeño que transfiere la llamada del Administrador de controladores al servidor. Su huella puede ser significativamente menor que los controladores ODBC totalmente funcionales en el servidor. En esta arquitectura, los recursos de cliente se pueden liberar si el servidor tiene más potencia informática. Además, la eficiencia y la seguridad de todo el sistema se pueden mejorar mediante la instalación de servidores de copia de seguridad y la realización de equilibrio de carga para optimizar el uso del servidor.
