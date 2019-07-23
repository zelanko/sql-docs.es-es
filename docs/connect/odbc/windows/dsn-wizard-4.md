---
title: Pantalla del Asistente para orígenes de datos (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 177888dd1034bb1edcb870db38b00bbc418cb261
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989457"
---
# <a name="data-source-wizard-screen-4"></a>Pantalla del Asistente para orígenes de datos 4

Especifique el idioma que se va a usar para los mensajes de SQL Server, la conversión del juego de caracteres y si el controlador ODBC para SQL Server debe utilizar la configuración regional. También puede controlar el registro de consultas de ejecución prolongada y la configuración de estadísticas de controlador.

## <a name="options"></a>Opciones

### <a name="change-the-language-of-sql-server-system-messages-to"></a>Establecer el siguiente idioma para los mensajes del sistema de SQL Server

Cada instancia de SQL Server puede tener varios conjuntos de mensajes del sistema, con cada uno en un idioma diferente (por ejemplo, inglés, español, francés, etc.). Si un origen de datos se define en un servidor que tiene varios conjuntos de mensajes del sistema, se puede especificar qué idioma desea utilizarse en ellos. En la lista, haga clic en el idioma. Esta opción no está disponible si solo hay instalado un idioma en SQL Server.

### <a name="use-strong-encryption-for-data"></a>Utilizar cifrado de alta seguridad para los datos

Cuando esta casilla está activada, los datos que se pasan a través de las conexiones que se realizan utilizando este DSN se cifran. De forma predeterminada los inicios de sesión se cifran, aun cuando la casilla esté desactivada.

### <a name="trust-server-certificate"></a>Certificado de servidor de confianza

Esta opción solo es aplicable cuando está habilitado el **uso de cifrado seguro para datos** . Cuando se selecciona, el certificado del servidor no se validará para tener el nombre de host correcto del servidor y debe ser emitido por una entidad de certificación de confianza. 

### <a name="perform-translation-for-character-data"></a>Realizar conversión de los datos de caracteres

Cuando esta casilla está activada, el controlador ODBC para SQL Server convierte las cadenas ANSI enviadas entre el equipo cliente y SQL Server utilizando Unicode. El controlador ODBC a veces realiza la conversión entre la página de códigos de SQL Server y Unicode en el equipo cliente. Esto requiere que la página de códigos utilizada por SQL Server esté disponible en el equipo cliente.

Cuando esta casilla está desactivada, no se efectúa ninguna conversión de caracteres extendidos en cadenas de caracteres ANSI cuando se envían entre la aplicación cliente y el servidor. Si el equipo cliente usa una página de códigos ANSI (ACP) diferente de la página de códigos de SQL Server, los caracteres extendidos de las cadenas de caracteres ANSI pueden interpretarse incorrectamente. Si el equipo cliente usa la misma página de códigos para su ACP que SQL Server, los caracteres extendidos se interpretan correctamente.

### <a name="use-regional-settings-when-outputting-currency-numbers-dates-and-times"></a>Usar la configuración regional cuando se muestren monedas, números, fechas y horas

Especifica que el controlador use la configuración regional del equipo cliente para dar formato a las monedas, números, fechas y horas en las cadenas de salida de caracteres. El controlador utiliza la configuración regional predeterminada para la cuenta de inicio de sesión de Windows del usuario que se conecta a través del origen de datos. Seleccione esta opción para las aplicaciones que solo muestran datos, no para las que los procesan.

### <a name="save-long-running-queries-to-the-log-file"></a>Guardar en el archivo de registro las consultas largas en ejecución

Especifica que el controlador registre cualquier consulta que tarde más de lo que indica el valor **Tiempo máximo de consulta**. Las consultas de ejecución prolongada se registran en el archivo especificado. Para especificar un archivo de registro, escriba la ruta de acceso completa y el nombre de archivo en el cuadro, o haga clic en **Examinar** para seleccionar un archivo de registro navegando por los directorios de archivos existentes.

### <a name="long-query-time-milliseconds"></a>Tiempo máximo de consulta (milisegundos)

Especifica un valor de umbral, en milisegundos, para el registro de consultas de ejecución prolongada. Se registran las consultas que tarden en ejecutarse mucho más de lo que indica esta cifra de milisegundos.

### <a name="log-odbc-driver-statistics-to-the-log-file"></a>Registrar estadísticas del controlador ODBC en el archivo de registro

Especifica que las estadísticas se registren. Las estadísticas se registran en el archivo especificado. Para especificar un archivo de registro, escriba la ruta de acceso completa y el nombre de archivo en el cuadro o haga clic en **Examinar** para seleccionar un archivo de registro navegando por los directorios de archivos existentes.

El registro de estadísticas es un archivo delimitado por tabuladores que se puede analizar en Microsoft Excel o en cualquier otra aplicación que admita archivos delimitados por tabuladores.

### <a name="connect-retry-count"></a>Recuento de reintentos de la conexión

Especifica el número de veces que se reintentará un intento de conexión incorrecta.

### <a name="connect-retry-interval-seconds"></a>Intervalo de reintento de conexión (segundos)

Especifica el número de segundos entre cada reintento de conexión. Para obtener más información sobre el funcionamiento de esta y las opciones de **número** de reintentos de conexión, consulte [resistencia de conexión en el controlador ODBC de Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).

### <a name="back"></a>Atrás

Haga clic en este botón para volver a la página anterior del asistente.

### <a name="finish"></a>Finalizar

Si la información especificada en esta pantalla se ha completado, puede hacer clic en **Finalizar**. El DSN se crea con todos los atributos especificados en esta y otras pantallas del asistente, y se le da la oportunidad de probar el DSN recién creado.

## <a name="next-steps"></a>Pasos siguientes

[Pantalla del Asistente para orígenes de datos 3](../../../connect/odbc/windows/dsn-wizard-3.md)
