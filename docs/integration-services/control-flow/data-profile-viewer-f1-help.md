---
title: "Visor de perfiles de datos (Ayuda F1) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "sql13.dts.dataprofileviewer.f1"
helpviewer_keywords: 
  - "Visor de perfiles de datos [Integration Services]"
  - "tarea de generación de perfiles de datos [Integration Services], visor"
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Visor de perfiles de datos (Ayuda F1)
  Utilice el Visor de perfil de datos para ver la salida de la Tarea de generación de perfiles de datos.  
  
 Para más información sobre cómo usar el Visor de perfil de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md). Para más información sobre cómo usar la Tarea de generación de perfiles de datos, que crea la salida del perfil que se analiza en el Visor de perfil de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
## Opciones estáticas  
 **Abrir**  
 Haga clic para buscar el archivo guardado que contiene la salida de la Tarea de generación de perfiles de datos.  
  
 Panel **Perfiles**  
 Expanda el árbol del panel **Perfiles** para ver los perfiles que están incluidos en la salida. Seleccione un perfil para ver los resultados de ese perfil.  
  
 Panel **Mensaje**  
 Muestra mensajes de estado.  
  
 Panel **Obtención de detalles**  
 Muestra las filas de datos que coinciden con un valor en la salida, si el origen de datos que usa la Tarea de generación de perfiles de datos está disponible.  
  
 Por ejemplo, si está viendo la salida de un perfil Distribución de valores de columna de una columna de estados americanos, el panel **Distribución de valor detallado** podría contener una fila para "WA". Haga doble clic en la fila en el panel **Distribución de valores detallados** para ver las filas de datos en las que el valor de la columna de estado sea "WA" en el panel de obtención de detalles.  
  
## Opciones dinámicas  
  
### Tipo de perfil = Perfil de distribución de longitud de columnas  
  
#### Perfil de distribución de longitud de columnas - panel \<columna>  
 **Longitud mínima**  
 Muestra la longitud mínima de los valores de esta columna.  
  
 **Longitud máxima**  
 Muestra la longitud máxima de los valores de esta columna.  
  
 **Omitir espacios iniciales**  
 Muestra si este perfil se calculó con un valor de **IgnoreLeadingSpaces** True o False. Esta propiedad se estableció en la página **Solicitudes de perfil** del Editor de tareas de generación de perfiles de datos.  
  
 **Omitir espacios finales**  
 Muestra si este perfil se calculó con un valor de **IgnoreTrailingSpaces** True o False. Esta propiedad se estableció en la página **Solicitudes de perfil** del Editor de tareas de generación de perfiles de datos.  
  
 **Recuento de filas**  
 Muestra el número de filas de la tabla o vista.  
  
#### Panel Distribución de longitud detallado  
 **Longitud**  
 Muestra las longitudes de columna encontradas en la columna de perfiles.  
  
 **Count**  
 Muestra el número de filas en las que el valor de la columna de perfiles tiene la longitud que se muestra en la columna **Longitud**.  
  
 **Porcentaje**  
 Muestra el porcentaje de filas en las que el valor de la columna de perfiles tiene la longitud que se muestra en la columna **Longitud**.  
  
### Tipo de perfil = Perfil de proporción de columnas nulas  
  
#### Perfil de proporción de columnas nulas - panel \<columna>  
 **Recuento nulo**  
 Muestra el número de filas en las que la columna de perfiles tiene el valor null.  
  
 **Porcentaje nulo**  
 Muestra el porcentaje de filas en las que la columna de perfiles tiene el valor null.  
  
 **Recuento de filas**  
 Muestra el número de filas de la tabla o vista.  
  
### Tipo de perfil = Perfil de patrón de columnas  
  
#### Perfil de patrón de columnas - panel \<columna>  
 **Recuento de filas**  
 Muestra el número de filas de la tabla o vista.  
  
#### Panel Distribución del patrón  
 **Patrón**  
 Muestra los patrones calculados para la columna de perfiles.  
  
 **Porcentaje**  
 Muestra el porcentaje de filas cuyos valores coinciden con el patrón que se muestra en la columna **Patrón**.  
  
### Tipo de perfil = Perfil de estadísticas de columnas  
  
#### Perfil de estadísticas de columnas - panel \<columna>  
 **Mínima**  
 Muestra el valor mínimo situado en la columna de perfiles.  
  
 **Máximo**  
 Muestra el valor máximo situado en la columna de perfiles.  
  
 **Promedio**  
 Muestra el promedio de los valores que se encuentran en la columna de perfiles.  
  
 **Desviación estándar**  
 Muestra la desviación estándar de los valores que se encuentran en la columna de perfiles.  
  
### Tipo de perfil = Perfil de distribución de valores de columna  
  
#### Perfil de distribución de valores de columna - panel \<columna>  
 **Número de valores distintos**  
 Muestra el recuento de valores distintos que se encuentran en la columna de perfiles.  
  
 **Recuento de filas**  
 Muestra el número de filas de la tabla o vista.  
  
#### Panel Distribución de valores detallado  
 **Value**  
 Muestra los distintos valores que se encuentran en la columna de perfiles.  
  
 **Count**  
 Muestra el número de filas en las que la columna de perfiles tiene el valor que se muestra en la columna **Valor**.  
  
 **Porcentaje**  
 Muestra el porcentaje de filas en las que la columna de perfiles tiene el valor que se muestra en la columna **Valor**.  
  
### Tipo de perfil = Perfil de claves candidatas  
  
#### Perfil de claves candidatas - panel \<tabla>  
 **Columnas de clave**  
 Muestra las columnas que se seleccionaron para los perfiles como clave candidata.  
  
 **Nivel de clave**  
 Muestra el nivel (como porcentaje) de la columna de clave candidata o de una combinación de columnas. Un nivel de clave menor del 100% indica que hay valores duplicados.  
  
#### Panel Infracciones de clave  
 **\<columna1>, \<columna2>, etc.**  
 Muestra los valores duplicados que se encontraron en la columna de perfiles.  
  
 **Count**  
 Muestra el número de filas en las que la columna especificada tiene el valor que se muestra en la primera columna.  
  
### Tipo de perfil = Perfil de dependencia funcional  
  
#### Panel Perfil de dependencia funcional  
 **Columnas determinantes**  
 Muestra la columna o columnas seleccionadas como columna determinante. En el ejemplo en el que el mismo código postal de Estados Unidos siempre debería tener el mismo estado, el código postal es la columna determinante.  
  
 **Columnas dependientes**  
 Muestra la columna o columnas seleccionadas como columna dependiente. En el ejemplo en el que el mismo código postal de Estados Unidos siempre debería tener el mismo estado, el estado es la columna dependiente.  
  
 **Nivel de dependencia funcional**  
 Muestra el nivel (como porcentaje) de la dependencia funcional entre las columnas. Un nivel de clave menor del 100% indica que hay casos en los que el valor determinante no determina el valor dependiente. En el ejemplo en el que el mismo código postal de Estados Unidos siempre debería tener el mismo estado, esto probablemente indica que algunos valores de estado no son válidos.  
  
#### Panel Infracciones de dependencia funcional  
  
> [!NOTE]  
>  Un porcentaje alto de valores erróneos en los datos podría provocar resultados inesperados en un perfil Dependencia funcional. Por ejemplo, el 90% de las filas tienen el valor "WI" como estado para el valor "98052" de código postal. El perfil notifica filas que contienen valor de estado correcto de "WA" como infracciones.  
  
 **\<nombre de columna determinante>**  
 Muestra el valor de la columna determinante o la combinación de columnas en esta infracción de la dependencia funcional.  
  
 **\<nombre de columna dependiente>**  
 Muestra el valor de la columna dependiente en esta infracción de la dependencia funcional.  
  
 **Recuento de soporte**  
 Muestra el número de filas en las que el valor de columna determinante determina la columna dependiente.  
  
 **Recuento de infracciones**  
 Muestra el número de filas en las que el valor de columna determinante no determina la columna dependiente. (Estas son las filas en las que el valor dependiente es el que se muestra en la columna **\<nombre de columna dependiente>**).  
  
 **Porcentaje admitido**  
 Muestra el porcentaje de filas en las que el valor de columna determinante determina la columna dependiente.  
  
### Tipo de perfil = Perfil de inclusión de valores  
  
#### Panel Perfil de inclusión de valores  
 **Columnas de subconjunto**  
 Muestra la columna o combinación de columnas que se incluyeron en el perfil para determinar si están en las columnas de superconjunto.  
  
 **Columnas de superconjunto**  
 Muestra la columna o combinación de columnas que se incluyeron en el perfil para determinar si incluyen los valores en las columnas de subconjunto.  
  
 **Nivel de inclusión**  
 Muestra el nivel (como porcentaje) de la superposición entre las columnas. Un nivel de clave menor que 100% indica que hay casos en los que el valor de subconjunto no se encuentra entre los valores del superconjunto.  
  
#### Panel Infracciones de inclusión  
 **\<columna1>, \<columna2>, etc.**  
 Muestra los valores en la columna o columnas del subconjunto que no se encontraban en la columna o columnas del superconjunto.  
  
 **Count**  
 Muestra el número de filas en las que la columna especificada tiene el valor que se muestra en la primera columna.  
  
## Vea también  
 [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md)   
 [Visor y tarea de generación de perfiles de datos](../../integration-services/control-flow/data-profiling-task-and-viewer.md)  
  
  