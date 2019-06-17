---
title: Comentarios sobre SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- sending feedback to Microsoft
- errors [SQL Server], feedback reporting
- feedback [SQL Server]
- submitting feedback [SQL Server]
- bug reporting [SQL Server]
- reporting usage information to Microsoft
- reporting errors to Microsoft
- SQL Server, feedback reporting
- documentation feedback [SQL Server]
- usage information reporting [SQL Server]
- product feedback [SQL Server]
- automatic error or usage reporting
ms.assetid: 28f3ebf0-ad71-4816-86a6-18a46f023cfe
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10466721f50dd8b090b5d6b1a06b5bffd6e5289d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62772283"
---
# <a name="providing-feedback-for-sql-server-2014"></a>Comentarios sobre SQL Server 2014
  [!INCLUDE[msCoName](../includes/msconame-md.md)] agradece que dedique parte de su tiempo a ayudarnos a mejorar nuestros productos y documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Puede transmitirnos sus sugerencias e informes de errores sobre las características e interfaz de usuario del producto, presentarnos sus comentarios acerca de la documentación y, si lo desea, enviarnos de manera automática sus informes de errores y datos de uso a [!INCLUDE[msCoName](../includes/msconame-md.md)] para su estudio. En el presente documento se describen las tres opciones para transmitirnos sus comentarios.  
  
## <a name="submitting-feedback-about-the-product"></a>Enviar comentarios acerca del producto  
 Puede usar la página de comentarios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect para enviar sus sugerencias e informar sobre errores acerca de las características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esto incluye características como herramientas y utilidades, lenguajes e interfaces de programación.  
  
 Puede encontrar la página de comentarios [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de muchas maneras.  
  
-   Vaya a la [página web](https://go.microsoft.com/fwlink/?linkid=34178) de comentarios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de [!INCLUDE[msCoName](../includes/msconame-md.md)] Connect.  
  
-   En la barra de herramientas Ayuda de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en el botón **Enviar comentarios** o seleccione el comando **Comunidad/Enviar comentarios**.  
  
-   En la barra de herramientas Ayuda de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic en el botón **Enviar comentarios**.  
  
-   En la parte superior de cualquier tema de los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], haga clic en el botón **Enviar comentarios**.  
  
 La barra de herramientas de ayuda no aparece en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ni en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] hasta que:  
  
-   Obtenga acceso a la ayuda desde la utilidad.  
  
-   Seleccione el **ayuda** casilla de verificación en la **las barras de herramientas** pestaña de la **herramientas/Personalizar...**  comando.  
  
## <a name="automatic-error-and-usage-reporting"></a>Informes automáticos de errores y usos  
 Puede habilitar determinadas características para notificar errores de manera automática y enviar información acerca de cómo utiliza el software y los servicios de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. [!INCLUDE[msCoName](../includes/msconame-md.md)] utiliza esta información para mejorar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Toda los datos se consideran información confidencial.  
  
### <a name="managing-automatic-usage-reporting"></a>Administrar el informe de errores automático  
 La elaboración automática de informes le permite tomar decisiones sobre la recopilación y envío de datos a [!INCLUDE[msCoName](../includes/msconame-md.md)]. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza dos canalizaciones para informar sobre los datos de uso. Ambas canalizaciones informan sobre datos similares, pero informan de los datos de uso en diferentes programas y se activan y desactivan de manera independiente. La activación o desactivación de una canalización mediante uno de los programas que la utiliza también detiene o inicia la recopilación de datos de otros programas con los que comparten la misma canalización.  
  
-   Una canalización se utiliza para informar de datos de uso de la totalidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], excepto para el componente Libros en pantalla y algunos de los elementos de la interfaz de usuario basados en [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio en las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Después de la instalación, también puede desactivar (o activar) esta canalización. Para ello, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra un proyecto basado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y después en el menú **Ayuda**, seleccione **Opciones de comentarios del cliente**. Este comando no aparecerá hasta que haya abierto un proyecto basado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   La otra canalización se utiliza para  los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], los elementos de la interfaz de usuario basados en Visual Studio de las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y Visual Studio. Después de la instalación, también puede desactivar (o activar) esta canalización. Para ello, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra un proyecto basado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y después en el menú **Ayuda**, seleccione **Opciones de comentarios del cliente**. Este comando no aparecerá hasta que haya abierto un proyecto basado en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="helping-build-a-better-books-online"></a>Ayudar a mejorar los Libros en pantalla  
 La habilitación de la creación de informes de uso para los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es de gran ayuda para que el equipo mejore el desarrollo de la documentación. La información nueva que recibimos nos ayuda a identificar las necesidades de los clientes. Nos ofrece la posibilidad de saber cómo se desplazan entre los temas, con qué frecuencia consultan determinados temas y cuáles son los que consideran más o menos útiles.  
  
 Sus comentarios nos permiten entender el uso que usted hace de la documentación. Ello nos ayuda a asignar nuestros recursos de producción escrita a los temas más importantes, así como a diseñar sistemas futuros de documentación para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Con esta información sobre el uso de Libros en pantalla también podemos identificar las características sobre las que los clientes buscan ayuda con más frecuencia. Con ello sabemos en qué áreas debemos aplicar mejoras para facilitar su uso.  
  
  
