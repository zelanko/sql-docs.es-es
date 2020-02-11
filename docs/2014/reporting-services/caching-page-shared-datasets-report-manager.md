---
title: Página de almacenamiento en caché, conjuntos de recursos compartidos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: eac372e9-d2a1-48a8-bbe5-09d101df16ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ae18d021465a7d14ea22b56534ea48ac316154c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109908"
---
# <a name="caching-page-shared-datasets-report-manager"></a>Página de almacenamiento en caché, conjuntos de datos compartidos (Administrador de informes)
  Use la página Propiedades de almacenamiento en caché para establecer las opciones de memoria caché de un conjunto de datos compartido.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Use el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario.  
  
### <a name="to-open-the-caching-properties-page-for-a-shared-dataset"></a>Para abrir la página Propiedades de almacenamiento en caché para un conjunto de datos compartido  
  
1.  Abra el Administrador de informes y busque el informe para el que desea configurar las propiedades del conjunto de datos compartido.  
  
2.  Señale al conjunto de datos compartido y haga clic en la flecha de lista desplegable.  
  
3.  En la lista desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales correspondiente al informe.  
  
4.  Haga clic en la pestaña de **almacenamiento en caché** .  
  
## <a name="options"></a>Opciones  
 **Almacenar en caché conjunto de datos compartido**  
 Coloca una copia temporal de los datos en una memoria caché cuando un usuario abre por primera vez un informe que usa este conjunto de datos compartido. Los usuarios siguientes que ejecuten el informe dentro del período de almacenamiento en caché reciben la copia en caché de los datos. El almacenamiento en memoria caché suele mejorar el rendimiento porque los datos se devuelven desde la memoria caché en lugar de ejecutarse de nuevo la consulta del conjunto de datos.  
  
 **Expirar la memoria caché después de este número de minutos**  
 Especifique el número de minutos durante los que guardar la copia en caché de los datos. Tan pronto como expire una copia temporal, los datos ya no se devolverán de la memoria caché. La próxima vez que un usuario abra un informe que use este conjunto de datos compartido, la consulta del conjunto de datos se ejecutará y el servidor de informes colocará de nuevo una copia de los datos actualizados en la memoria caché.  
  
 **Expirar la memoria caché según la siguiente programación.**  
 Programe el tiempo en el que los datos en caché dejarán de ser válidos y se quitarán de la memoria caché. La programación puede ser compartida o puede ser una específica solamente para el conjunto de datos compartido actual.  
  
 **Programación específica del conjunto de datos**  
 Especifique una programación que solo use este conjunto de datos.  
  
 **Programación compartida**  
 Especifique una programación que se comparta entre los informes, suscripciones y otros conjuntos de datos compartidos.  
  
 **Aplicar**  
 Guarde los cambios.  
  
## <a name="see-also"></a>Consulte también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes la ayuda F1](../../2014/reporting-services/report-manager-f1-help.md)   
 [Almacenar en caché conjuntos de recursos compartidos &#40;SSRS&#41;](report-server/cache-shared-datasets-ssrs.md)   
 [Programaciones](subscriptions/schedules.md)  
  
  
