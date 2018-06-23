---
title: Formatos de fecha y hora | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c5c223189964ee9c9bdcd471d64275838ba65d70
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105439"
---
# <a name="date-and-time-formats"></a>Formatos de fecha y hora
  El análisis rápido ofrece un conjunto rápido y simple de rutinas para analizar datos. El análisis rápido admite los siguientes formatos para los tipos de datos de fecha y hora.  
  
## <a name="date-data-types"></a>Tipos de datos de fecha  
 El análisis rápido admite los siguientes formatos de cadena para tipos de datos de fecha:  
  
-   Formatos de fecha con espacios en blanco iniciales. Por ejemplo, el valor " 2004- 02-03" es válido.  
  
-   Formatos ISO 8601, que se muestran en la tabla siguiente:  
  
    |Formato|Descripción|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|Los formatos básico y extendido para un año de cuatro dígitos, un mes de dos dígitos y un día de dos dígitos. En el formato extendido, las partes de la fecha se encuentran separadas por guiones (-).|  
    |YYYY-MM|Formatos básico y extendido de precisión reducida para un año de cuatro dígitos y un mes de dos dígitos. En el formato extendido, las partes de la fecha se encuentran separadas por guiones (-).|  
    |YYYY|El formato de precisión reducida es un año de cuatro dígitos.|  
  
 El análisis rápido no admite los siguientes formatos para datos de fecha:  
  
-   Valores alfabéticos de meses. Por ejemplo, el formato de fecha Oct-31-2003 no es válido.  
  
-   Formatos ambiguos como DD-MM-YYYY y MM-DD-YYYY. Por ejemplo, las fechas 03-04-1995 y 04-03-1995 no son válidas.  
  
-   Formatos truncados básico y extendido para un año natural de cuatro dígitos y un día de tres dígitos dentro de un año, YYYYDDD y YYYY-DDD.  
  
-   Formatos básico y extendido para un año de cuatro dígitos, un número de dos dígitos para la semana del año y un número de un dígito para el día de la semana, YYYYWwwD y YYYY-Www-D.  
  
-   Los formatos truncados básico y extendido para un año y una semana son un año de cuatro dígitos y un número de dos dígitos para la semana, YYYWww y YYYY-Www.  
  
 El análisis rápido genera los datos como DT_DBDATE. Los valores de fechas en formatos truncados se rellenan. Por ejemplo, YYYY pasa a ser YYYY0101.  
  
 Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
## <a name="time-data-type"></a>Tipo de datos de hora  
 El análisis rápido admite los siguientes formatos de cadena para tipos de datos de hora:  
  
-   Formatos de hora con espacios en blanco iniciales. Por ejemplo, el valor " 10:24" es válido.  
  
-   Formato de 24 horas El análisis rápido no admite la notación AM y PM.  
  
-   Formatos de hora ISO 8601, que se muestran en la tabla siguiente:  
  
    |Formato|Descripción|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|Los formatos básico y extendido para una hora de dos dígitos, minutos de dos dígitos y segundos de dos dígitos. En el formato extendido, las partes de la hora se encuentran separadas por dos puntos (:).|  
    |HHMI<br /><br /> HH:MI|Formatos truncados básico y extendido para una hora de dos dígitos y minutos de dos dígitos. En el formato extendido, las partes de la hora se encuentran separadas por dos puntos (:).|  
    |HH|Formato truncado para una hora de dos dígitos.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|Formato para medianoche.|  
  
-   Formatos de hora que especifican una zona horaria, como se muestra en la tabla siguiente:  
  
    |Formato|Descripción|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|Formatos básicos y extendidos que indican el número de horas y minutos que se agregan a la hora universal coordinada (UTC) para obtener la hora local.|  
    |-HH:MI<br /><br /> -HHMI|Formatos básicos y extendidos que indican el número de horas y minutos que se restan a la UTC para obtener la hora local.|  
    |+HH|Formato truncado que indica el número de horas que se agregan a la UTC para obtener la hora local.|  
    |-HH|Formato truncado que indica el número de horas que se restan a la UTC para obtener la hora local.|  
    |Z|Un valor de 0 que indica que la hora se representa en UTC.|  
  
     Los formatos para todos los datos de fecha/hora pueden incluir un elemento de zona horaria. Sin embargo, el sistema omite el valor de zona horaria, excepto cuando los datos son del tipo DT_DBTIMESTAMPOFFSET. Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
     En formatos que incluyen un elemento de zona horaria, no hay ningún espacio entre el elemento de tiempo y el elemento de zona horaria, como se muestra en el ejemplo siguiente:  
  
     HH:MI:SS[+HH:MI]  
  
     Los corchetes del ejemplo anterior indican que el valor de zona horaria es opcional.  
  
-   Formatos de hora que incluyen una fracción decimal, como se muestra en la tabla siguiente:  
  
    |Formato|Descripción|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n es un valor entre 0 y 9999999 que representa una fracción de horas. Los corchetes indican que este valor es opcional.<br /><br /> Por ejemplo, el valor 12.750 indica 12:45.|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n es un valor entre 0 y 9999999 que representa una fracción de minutos. Los corchetes indican que este valor es opcional.<br /><br /> Por ejemplo, el valor 1220.500 indica 12:20:30.|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n es un valor entre 0 y 9999999 que representa una fracción de segundos. Los corchetes indican que este valor es opcional.<br /><br /> Por ejemplo, el valor 122040.250 indica 12:20:40.15.|  
  
    > [!NOTE]  
    >  El separador decimal para los formatos de hora de la tabla anterior puede ser un punto o una coma.  
  
-   Valores de hora que incluyen un segundo intercalar, como se muestra en los ejemplos siguientes:  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 El análisis rápido genera cadenas como DT_DBTIME y DT_DBTIME2. Los valores de horas en formatos truncados se rellenan. Por ejemplo, HH:MI pasa a ser HH:MM:00.000.  
  
 Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
## <a name="datetime-data-type"></a>Tipo de datos de fecha/hora  
 El análisis rápido admite los siguientes formatos de cadena para tipos de datos de fecha/hora:  
  
-   Formatos con espacios en blanco iniciales. Por ejemplo, el valor "  2003-01/10T203910" es válido.  
  
-   Combinaciones de formatos de fecha válidos y los formatos de hora válidos separados por una T mayúscula, y formatos de zona horaria válidos, como YYYYMMDDT[HHMISS][+HH:MI]. Los valores de hora y zona horaria no son obligatorios. Por ejemplo, "2003-10-14" es válido.  
  
 El análisis rápido no admite intervalos de tiempo. Por ejemplo, un intervalo de tiempo identificado con una fecha y hora de inicio y fin en el formato YYYYMMDDThhmmss/YYYYMMDDThhmmss no se puede analizar.  
  
 El análisis rápido genera cadenas como DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 y DT_DBTIMESTAMPOFFSET. Los valores de fecha/hora en formatos truncados se rellenan. En la siguiente tabla se muestran los valores que se agregan para las partes de fecha y hora que faltan.  
  
|Parte de fecha y hora|Relleno|  
|---------------------|-------------|  
|Segundos|Agregar 00.|  
|Minutos|Agregar 00:00.|  
|Hour|Agregar 00:00:00.|  
|Day|Agregar 01 para el día del mes.|  
|Month|Agregar 01 para el mes del año.|  
  
 Para más información, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
  