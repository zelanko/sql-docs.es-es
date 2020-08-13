---
title: Uso de los KPI en Reporting Services | Microsoft Docs
description: Obtenga información sobre cómo puede medir fácilmente el estado y el rendimiento mediante el uso de KPI en SQL Server Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.date: 07/02/2017
ms.openlocfilehash: b92f19c74e5b5e3215836e174bf895f7cb61c36b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247444"
---
# <a name="working-with-kpis-in-reporting-services"></a>Uso de los KPI en Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Un *indicador clave de rendimiento (KPI)* es una indicación visual que transmite la cantidad de progreso realizado hacia la consecución de un objetivo.  Los indicadores clave de rendimiento sirven para que los equipos, los administradores y las empresas evalúen rápidamente el progreso realizado frente a objetivos cuantificables.
  
Si usa KPI en SQL Server Reporting Services, podrá visualizar rápidamente las respuestas a las preguntas siguientes:  
  
- ¿Voy adelantado o atrasado?  
  
- ¿Qué adelanto o atraso llevo?  
  
- ¿Cuáles son las cantidades mínimas que ha completado?  

> [!NOTE]
> Solo se puede obtener acceso a los KPI en las ediciones Enterprise (Developer) del portal SSRS.

## <a name="creating-a-dataset"></a>Creación de un conjunto de datos

Un KPI solo utilizará la primera fila de datos de un conjunto de datos compartido. Asegúrese de que los datos que desea utilizar se encuentran en la primera fila. Para crear un conjunto de datos compartido, puede utilizar el Generador de informes o SQL Server Data Tools.  
  
> **Nota**: El conjunto de datos no tiene que estar en la misma carpeta que el KPI.  
  
## <a name="placement-of-kpis"></a>Ubicación de los KPI  
  
Los KPI pueden crearse en cualquier carpeta de su servidor de informes.  Antes de crear un KPI, deberá tener clara la ubicación correcta donde colocarlo. Puede colocarlo en una carpeta que sea visible para los usuarios y a la vez pertinente para otros informes y KPI relacionados.  
## <a name="adding-a-kpi"></a>Adición de un KPI
  
Después de determinar la ubicación de los KPI, vaya a la carpeta y seleccione **Nuevo** > **KPI** en el menú superior.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
Así se abrirá la pantalla **Nuevo KPI** .  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Puede asignar valores estáticos o utilizar los datos de un conjunto de datos compartido. Al crear un nuevo KPI, se rellenará con un conjunto aleatorio de datos manuales.  
  
| Campo | Descripción |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| Formato del valor | Se utiliza para cambiar el formato del valor que se muestra. |
| Value | El valor para mostrar del KPI. |
| Objetivo | Se utiliza como comparación con un valor numérico y se muestra en forma de diferencia porcentual. |
| Estado | Valor numérico que se usa para determinar el color del icono de KPI. Los valores válidos son 1 (verde), 0 (ámbar) y -1 (rojo). |
| Conjunto de tendencias | Valores numéricos separados por comas usados para la visualización de gráficos. También puede establecerse en una columna de un conjunto de datos con valores que representen la tendencia. |
| Contenido relacionado | La capacidad de establecer un vínculo detallado. Este vínculo puede ser un informe móvil publicado en el portal o una dirección URL personalizada. |
  
> **Advertencia**: Aunque puede usar el valor de palabra para el campo **Estado** en tiempo de diseño, debe utilizar el valor de número si va a actualizar un conjunto de datos. Si actualiza un conjunto de datos con el valor de palabra, en lugar del de número, se podría dañar los KPI en el servidor.  
>
> **Nota**: Los campos **Valor**, **Objetivo** y **Estado** solo pueden elegir un valor de la primera fila del resultado de un conjunto de datos. El campo **Trend set** (Conjunto de tendencias), sin embargo, puede elegir qué columna refleja la tendencia.  
  
Para usar datos de un conjunto de datos compartido, puede realizar los siguientes pasos:
  
1. Cambie el valor del cuadro desplegable del campo de **Set manually**(Establecer manualmente), o **Not set**(No establecido), a **Dataset field**(Campo de conjunto de datos).  
  
    ![rsCreateKPI3](../reporting-services/media/rscreatekpi3.png)  
  
2. Haga clic en los **puntos suspensivos (...)** en el cuadro de datos. Se abrirá la pantalla **Pick a Dataset** (Elegir un conjunto de datos).  
  
    ![rsCreateKPI4](../reporting-services/media/rscreatekpi4.png)  
  
3. Seleccione el conjunto de datos que contenga los datos que desea mostrar.  
  
4. Elija el campo que desea usar. Seleccione **Aceptar**.  
  
    ![rsCreateKPI5](../reporting-services/media/rscreatekpi5.png)  
  
5. Cambie **Value format** (Formato de valor) para que coincida con el formato del valor. En este ejemplo, el valor es una moneda.  
  
    ![rsCreateKPI6](../reporting-services/media/rscreatekpi6.png)  
  
6. Seleccione **Aplicar**.  
  
    ![rsCreateKPI7](../reporting-services/media/rscreatekpi7.png)

## <a name="configuring-related-content"></a>Configuración de contenido relacionado

Al elegir **Informe móvil**, puede elegir el destino en un cuadro de diálogo.

   ![Informe móvil](media/rscreatekpi-related-content-mobile-report.png)

Al hacer clic ahora en el KPI del portal, aparece una miniatura del informe móvil en el menú desplegable de contenido relacionado. Al hacer clic en esta miniatura, puede ir directamente a este informe.

También puede especificar una dirección URL personalizada. Esta tarea puede ser cualquier cosa: un sitio web, un sitio de SharePoint, una dirección URL de un informe SSRS (que le permitiría pasar parámetros codificados de forma rígida).

![Dirección URL personalizada](media/rscreatekpi-related-content-custom-url.png)

Al hacer clic ahora en el KPI, la dirección URL aparece en el contenido relacionado.

Solo es posible agregar un informe móvil o una dirección URL personalizada.
  
## <a name="removing-a-kpi"></a>Eliminación de un KPI  
  
Para quitar un KPI, puede realizar los siguientes pasos.
  
1. Haga clic en los **puntos suspensivos (...)** del KPI que quiera quitar. Seleccione **Administrar**.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2. Seleccione **Eliminar**. Vuelva a seleccionar **Eliminar** en el cuadro de diálogo de confirmación.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Actualización de un KPI  
  
Para actualizar el KPI, tendrá que configurar un almacenamiento en caché para el conjunto de datos compartido. Para más información sobre los planes de actualización de la memoria caché, vea [Work with Shared Datasets](../reporting-services/work-with-shared-datasets-web-portal.md) (Trabajar con conjuntos de datos compartidos).  
  
## <a name="next-steps"></a>Pasos siguientes
  
[Portal web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabajo con conjuntos de datos compartidos](../reporting-services/work-with-shared-datasets-web-portal.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
