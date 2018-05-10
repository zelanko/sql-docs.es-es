---
title: Uso de los KPI en Reporting Services | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a28cf500-6d47-4268-a248-04837e7a09eb
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 74c0cd02499ab10f2aeded7cc528c7db244cd2cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-kpis-in-reporting-services"></a>Uso de los KPI en Reporting Services

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Un indicador clave de rendimiento (KPI) es una indicación visual que transmite la cantidad de progreso realizado hacia la consecución de un objetivo.  Los indicadores clave de rendimiento sirven para que los equipos, los administradores y las empresas evalúen rápidamente el progreso realizado frente a objetivos cuantificables.   
  
Si utiliza KPI en SQL Server 2016, podrá visualizar rápidamente las respuestas a las siguientes preguntas:  
  
-   ¿Voy adelantado o atrasado?  
  
-   ¿Qué adelanto o atraso llevo?  
  
-   ¿Cuál es el progreso mínimo completado?  
  
## <a name="creating-a-dataset"></a>Creación de un conjunto de datos  
Un KPI solo utilizará la primera fila de datos de un conjunto de datos compartido. Asegúrese de que los datos que desea utilizar se encuentran en la primera fila. Para crear un conjunto de datos compartido, puede utilizar el Generador de informes o SQL Server Data Tools.  
  
> **Nota**: El conjunto de datos no tiene que estar en la misma carpeta que el KPI.  
  
## <a name="placement-of-kpis"></a>Ubicación de los KPI  
  
Los KPI pueden crearse en cualquier carpeta de su servidor de informes.  Antes de crear un KPI, deberá tener clara la ubicación correcta donde colocarlo. Se recomienda colocarlo en una carpeta que sea visible para los usuarios y a la vez pertinente para otros informes y KPI relacionados.  
  
## <a name="adding-a-kpi"></a>Adición de un KPI  
  
Después de determinar la ubicación de los KPI, vaya a la carpeta y seleccione **Nuevo** > **KPI** en el menú superior.  
  
![rsCreateKPI1](../reporting-services/media/rscreatekpi1.png)  
  
Así se abrirá la pantalla **Nuevo KPI** .  
  
![rsCreateKPI2](../reporting-services/media/rscreatekpi2.png)  
  
Puede asignar valores estáticos o utilizar los datos de un conjunto de datos compartido. Al crear un nuevo KPI, se rellenará con un conjunto aleatorio de datos manuales.  
  
|Campo|Description|  
|---|---|  
|Formato del valor|  Se utiliza para cambiar el formato del valor que se muestra.|   
|Valor|El valor para mostrar del KPI.|  
|Objetivo|Se utiliza como comparación con un valor numérico y se muestra en forma de diferencia porcentual.|  
|Estado|Valor numérico que se usa para determinar el color del icono de KPI. Los valores válidos son 1 (verde), 0 (ámbar) y -1 (rojo).|  
|Conjunto de tendencias|Valores numéricos separados por comas usados para la visualización de gráficos. También puede establecerse en una columna de un conjunto de datos con valores que representen la tendencia.|  
  
> **Advertencia**: Aunque puede usar el valor de palabra para el campo **Estado** en tiempo de diseño, debe utilizar el valor de número si va a actualizar un conjunto de datos. Si actualiza un conjunto de datos con el valor de palabra, en lugar del de número, se podría dañar los KPI en el servidor.  
  
> **Nota**: Los campos **Valor**, **Objetivo** y **Estado** solo pueden elegir un valor de la primera fila del resultado de un conjunto de datos. El campo **Trend set** (Conjunto de tendencias), sin embargo, puede elegir qué columna refleja la tendencia.  
  
Para utilizar datos de un conjunto de datos compartido, puede realizar lo siguiente:  
  
1.  Cambie el valor del cuadro desplegable del campo de **Set manually**(Establecer manualmente), o **Not set**(No establecido), a **Dataset field**(Campo de conjunto de datos).  
  
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
  
## <a name="removing-a-kpi"></a>Eliminación de un KPI  
  
Para quitar un KPI, puede hacer lo siguiente.  
  
1.  Seleccione **...** (los puntos suspensivos) del KPI que quiere quitar. Seleccione **Administrar**.  
  
    ![rsRemoveKPI1](../reporting-services/media/rsremovekpi1.png)  
  
2.  Seleccione **Eliminar**. Vuelva a seleccionar **Eliminar** en el cuadro de diálogo de confirmación.  
  
    ![rsRemoveKPI2](../reporting-services/media/rsremovekpi2.png)  
  
## <a name="refreshing-a-kpi"></a>Actualización de un KPI  
  
Para actualizar el KPI, tendrá que configurar un almacenamiento en caché para el conjunto de datos compartido. Para más información sobre los planes de actualización de la memoria caché, vea [Work with Shared Datasets](../reporting-services/work-with-shared-datasets-web-portal.md) (Trabajar con conjuntos de datos compartidos).  
  
## <a name="next-steps"></a>Pasos siguientes
  
[Portal web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabajo con conjuntos de datos compartidos](../reporting-services/work-with-shared-datasets-web-portal.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
