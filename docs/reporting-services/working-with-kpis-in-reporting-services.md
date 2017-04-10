---
title: "Uso de los KPI en Reporting Services | Microsoft Docs"
ms.date: "02/24/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# Uso de los KPI en Reporting Services
Un indicador clave de rendimiento (KPI) es una indicación visual que transmite la cantidad de progreso realizado hacia la consecución de un objetivo.  Los indicadores clave de rendimiento sirven para que los equipos, los administradores y las empresas evalúen rápidamente el progreso realizado frente a objetivos cuantificables.   
  
Si utiliza KPI en SQL Server 2016, podrá visualizar rápidamente las respuestas a las siguientes preguntas:  
  
-   ¿Voy adelantado o atrasado?  
  
-   ¿Qué adelanto o atraso llevo?  
  
-   ¿Cuál es el progreso mínimo completado?  
  
## Creación de un conjunto de datos  
Un KPI solo utilizará la primera fila de datos de un conjunto de datos compartido. Asegúrese de que los datos que desea utilizar se encuentran en la primera fila. Para crear un conjunto de datos compartido, puede utilizar el Generador de informes o SQL Server Data Tools.  
  
> **Nota**: El conjunto de datos no tiene que estar en la misma carpeta que el KPI.  
  
## Ubicación de los KPI  
  
Los KPI pueden crearse en cualquier carpeta de su servidor de informes.  Antes de crear un KPI, deberá tener clara la ubicación correcta donde colocarlo. Se recomienda colocarlo en una carpeta que sea visible para los usuarios y a la vez pertinente para otros informes y KPI relacionados.  
  
## Adición de un KPI  
  
Después de determinar la ubicación de los KPI, vaya a la carpeta y seleccione **Nuevo** > **KPI** en el menú superior.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
Así se abrirá la pantalla **Nuevo KPI**.  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Puede asignar valores estáticos o utilizar los datos de un conjunto de datos compartido. Al crear un nuevo KPI, se rellenará con un conjunto aleatorio de datos manuales.  
  
|Campo|Description|  
|---|---|  
|Formato del valor|  Se utiliza para cambiar el formato del valor que se muestra.|   
|Value|El valor para mostrar del KPI.|  
|Objetivo|Se utiliza como comparación con un valor numérico y se muestra en forma de diferencia porcentual.|  
|Estado|Valor numérico que se usa para determinar el color del icono de KPI. Los valores válidos son 1 (verde), 0 (ámbar) y -1 (rojo).|  
|Conjunto de tendencias|Valores numéricos separados por comas usados para la visualización de gráficos. También puede establecerse en una columna de un conjunto de datos con valores que representen la tendencia.|  
  
> **Advertencia**: Aunque puede usar el valor de palabra para el campo **Estado** en tiempo de diseño, debe utilizar el valor de número si va a actualizar un conjunto de datos. Si actualiza un conjunto de datos con el valor de palabra, en lugar del de número, se podría dañar los KPI en el servidor.  
  
> **Nota**: Los campos **Valor**, **Objetivo** y **Estado** solo pueden elegir un valor de la primera fila del resultado de un conjunto de datos. El campo **Trend set** (Conjunto de tendencias), sin embargo, puede elegir qué columna refleja la tendencia.  
  
Para utilizar datos de un conjunto de datos compartido, puede realizar lo siguiente:  
  
1.  Cambie el valor del cuadro desplegable del campo de **Set manually** (Establecer manualmente), o **Not set** (No establecido), a **Dataset field** (Campo de conjunto de datos).  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2.  Seleccione **…** (los puntos suspensivos) en el cuadro de datos. Se abrirá la pantalla **Pick a Dataset** (Elegir un conjunto de datos).  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3.  Seleccione el conjunto de datos que contenga los datos que desea mostrar.  
  
4.  Elija el campo que desea usar. Seleccione **Aceptar**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5.  Cambie **Value format** (Formato de valor) para que coincida con el formato del valor. En este ejemplo, el valor es una moneda.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6.  Seleccione **Aplicar**.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)  
  
## Eliminación de un KPI  
  
Para quitar un KPI, puede hacer lo siguiente.  
  
1.  Seleccione **...** (los puntos suspensivos) del KPI que desea quitar. Seleccione **Administrar**.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  Seleccione **Eliminar**. Vuelva a seleccionar **Eliminar** en el cuadro de diálogo de confirmación.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## Actualización de un KPI  
  
Para actualizar el KPI, tendrá que configurar un **plan de actualización de caché** el conjunto de datos compartido. Actualmente, no es posible configurar un plan de actualización de caché desde el portal web. Debe ir al antiguo Administrador de informes para hacerlo.   
  
Este lo guiará por los pasos necesarios para configurar un plan de actualización de caché con algunas opciones básicas. Para obtener más información sobre los planes de actualización de caché, consulte [Opciones de actualización de memoria caché (Administrador de informes)](Cache%20Refresh%20Options%20(Report%20Manager).xml).  
  
1.  Abra el Administrador de informes y busque el conjunto de datos compartido para el que desea configurar las propiedades del plan de actualización de caché.   
  
2.  Pase el mouse por encima del informe o el conjunto de datos compartido, y seleccione la flecha de lista desplegable.  
  
3.  En la lista desplegable, seleccione **Administrar**. Se abrirá la página **Propiedades generales**.  
  
4.  Seleccione la pestaña **Opciones de actualización de caché**.  
  
5.  Para crear un nuevo plan de memoria caché, haga clic en **Nuevo plan de actualización de caché**.  
  
    ![rsRefreshKPI1](../reporting-services/media/rsrefreshkpi1.png)  
  
6.  Se le mostrará un mensaje donde se le pregunta si desea habilitar el almacenamiento en caché para este elemento con las opciones predeterminadas. Elija **Aceptar**.  
  
    > **Nota:** Debe habilitar e iniciar el servicio del Agente SQL Server para crear un plan de actualización de caché.  
  
7.  Puede elegir una programación específica o seleccionar una compartida, si existe alguna.  
  
8.  Los valores del KPI se actualizarán cuando se ejecute la programación del plan de actualización de caché.  
  
    ![rsRefreshKPI2](../reporting-services/media/rsrefreshkpi2.png)  
  
## Vea también  
  
- [Portal web (modo nativo de SSRS)](../reporting-services/web-portal-ssrs-native-mode.md)  
  
- [Opciones de actualización de memoria caché (Administrador de informes)](Cache%20Refresh%20Options%20(Report%20Manager).xml)  
  
    
  
  
  
