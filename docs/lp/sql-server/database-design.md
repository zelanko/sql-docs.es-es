---
layout: HubPage
hide_bc: true
title: Diseño de base de datos de SQL Server
description: Descubra las características de SQL Server que le ayudarán a diseñar la base de datos que mejor se adapte a sus necesidades empresariales.
ms.topic: hub-page
ms.prod: sql
author: MashaMSFT
ms.author: mathoma
ms.date: 12/15/2018
featureFlags:
- clicktale
ms.openlocfilehash: c08b067a8c92b7fea32b53cd8b14b7ecc13272d0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077245"
---
<div id="main" class="v2">
    <div class="container">
        <ul class="cardsY panelContent featuredContent">
            <li>
                <a href="https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-ctp">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-sql-server.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Probar SQL Server 2019 (versión preliminar)</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/get-azure-sql-vm.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Obtener una máquina virtual con SQL Server</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>
            <li>
                <a href="/sql/ssms/download-sql-server-management-studio-ssms">
                    <div class="cardSize">
                        <div class="cardPadding">
                            <div class="card">
                                <div class="cardImageOuter">
                                    <div class="cardImage">
                                        <img src="media/index/download-ssms.svg" alt="" />
                                    </div>
                                </div>
                                <div class="cardText">
                                    <span class="likeAnH3">Descargar SQL Server Management Studio</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </a>
            </li>              
        </ul>
    </div>
    <div class="container">
        <h1>SQL Server: Diseño de la base de datos</h1>
        <ul class="pivots tabLess">
            <li class="pivotItem" style="display: list-item;" data-id="#products">
                <a href="#products" data-linktype="self-bookmark"></a>
                <ul id="products">
                    <li class="panelItem" data-index="0">
                        <a class="singlePanelNavItem selected" href="#products1" data-linktype="self-bookmark"></a>
                        <ul class="cardsD panelContent singlePanelContent" id="products1" style="margin-top: 0px; display: flex;">
                            <li>
                                <a href="/sql/relational-databases/collations/collation-and-unicode-support/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/collation.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Intercalación</h3>
                                                    <p>Las intercalaciones de SQL Server proporcionan propiedades de distinción entre mayúsculas y minúsculas, acentos y reglas de ordenación para los datos. Las intercalaciones que se utilizan con tipos de datos de caracteres como char y varchar dictan la página de códigos y los caracteres correspondientes que se pueden representar para ese tipo de datos. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/databases/databases/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/databases.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Bases de datos</h3>
                                                    <p>Una base de datos de SQL Server consta de una colección de tablas en las que se almacena un conjunto específico de datos estructurados. Una tabla contiene una colección de filas, también denominadas tuplas o registros, y columnas, también denominadas atributos.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> <li>
                                <a href="/sql/relational-databases/blob/filestream-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filestream.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Secuencia de archivos</h3>
                                                    <p>La secuencia de archivos permite a las aplicaciones basadas en SQL Server almacenar datos no estructurados, como documentos e imágenes, en el sistema de archivos.  </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/blob/filetables-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/filetable.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Tabla de archivos</h3>
                                                    <p>La tabla de archivos permite que una aplicación pueda integrar sus componentes de administración de datos y almacenamiento, así como proporcionar servicios de SQL Server integrados (incluidas la búsqueda de texto completo y la búsqueda semántica) en datos y metadatos no estructurados.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/graphs/sql-graph-overview/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sql-graphs.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Gráfico</h3>
                                                    <p>Una base de datos de gráficos es una colección de nodos (o vértices) y bordes (o relaciones). Un nodo representa una entidad (por ejemplo, una persona o una organización) y un borde representa una relación entre los dos nodos que conecta (por ejemplo, gustos o amigos). </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/hierarchical-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/hierarchy-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Datos jerárquicos</h3>
                                                    <p>Los datos jerárquicos se definen como un conjunto de elementos de datos que se relacionan entre sí mediante relaciones jerárquicas. Las relaciones jerárquicas existen allí donde un elemento de los datos es el elemento primario de otro elemento.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/indexes/indexes/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/indexes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Índices</h3>
                                                    <p>Información general del otro tipo de índices que usa SQL para organizar los datos. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/sequence-numbers/sequence-numbers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/sequence-numbers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Números de secuencia</h3>
                                                    <p>Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según la especificación con la que se creó la secuencia.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/spatial/spatial-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/spatial-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Datos espaciales</h3>
                                                    <p>Los datos espaciales representan información sobre la ubicación física y la forma de objetos geométricos. Estos objetos pueden ser ubicaciones de punto u objetos más complejos como países, carreteras o lagos. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/stored-procedures/stored-procedures-database-engine/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/stored-procedures.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Procedimientos almacenados</h3>
                                                    <p>Un procedimiento almacenado de SQL Server es un grupo de una o varias instrucciones Transact-SQL o una referencia a un método de Common Runtime Language (CLR) de Microsoft .NET Framework. Los procedimientos se asemejan a las construcciones de otros lenguajes de programación.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                            <li>
                                <a href="/sql/relational-databases/tables/tables/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/tables.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Tablas</h3>
                                                    <p>Las tablas son objetos de base de datos que contienen todos sus datos. En las tablas, los datos se organizan con arreglo a un formato de filas y columnas, similar al de una hoja de cálculo. Cada fila representa un registro único y cada columna un campo dentro del registro.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/track-changes/track-data-changes-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/track-changes.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Seguimiento de cambios</h3>
                                                    <p>Información general de dos características que permiten el seguimiento de datos: captura de datos modificados y seguimiento de cambios.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/triggers/logon-triggers/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/triggers.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Desencadenadores</h3>
                                                    <p>Los desencadenadores permiten una respuesta automatizada a una acción específica, como un inicio de sesión o un comando de modificación de base de datos. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>
                            <li>
                                <a href="/sql/relational-databases/views/views/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/views.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>Vistas</h3>
                                                    <p>Una vista es una tabla virtual cuyo contenido está definido por una consulta.</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li>  
                            <li>
                                <a href="/sql/relational-databases/xml/xml-data-sql-server/">
                                    <div class="cardSize">
                                        <div class="cardPadding">
                                            <div class="card">
                                                <div class="cardImageOuter">
                                                    <div class="cardImage">
                                                        <img src="media/database-design/xml-data.svg" alt="" />
                                                    </div>
                                                </div>
                                                <div class="cardText">
                                                    <h3>datos XML</h3>
                                                    <p>Información general de lo que se puede hacer con el tipo de datos XML, los índices XML, las colecciones de esquemas XML y mucho más. </p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </a>
                            </li> 
                                    <li>
                                      <a href="/sql/lp/sql-server/query-data/">
                                          <div class="cardSize">
                                              <div class="cardPadding">
                                                  <div class="card">
                                                      <div class="cardImageOuter">
                                                          <div class="cardImage">
                                                              <img src="media/index/query-data.svg" alt="" /> 
                                                          </div>
                                                      </div>
                                                      <div class="cardText">
                                                          <h3>Datos de consultas</h3>
                                                          <p><b>Cursores, sinónimos, scripting, combinaciones, funciones definidas por el usuario, búsqueda de texto completo </b></p>
                                                      </div>
                                                  </div>
                                              </div>
                                          </div>
                                      </a>
                                    </li>
                        </ul>
                    </li>
                </ul>
            </li>
        </ul>
    </div>
</div>
<div class="container centered pageFooter">
        <h2>Manténgase en contacto con nosotros</h2>
        <ul class="links">
           <li>
                <a href="https://aka.ms/editsqldocs" data-linktype="external"> Contribuir </a>
            </li>
           <li>
                <a href="https://docs.microsoft.com/sql/sql-server/sql-server-get-help" data-linktype="external"> Obtener ayuda </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsfeedback" data-linktype="external"> Comentarios </a>
            </li>
           <li>
                <a href="https://aka.ms/sqldocsurvey" data-linktype="external"> Encuesta </a>
            </li>
           <li>
                <a href="https://cloudblogs.microsoft.com/sqlserver/" data-linktype="external"> Blog </a>
            </li>
            <li>
                <a href="https://twitter.com/sqldocs" data-linktype="external"> Twitter </a>
            </li>
            <li>
                <a href="https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqldatabaseengine&filter=alltypes&sort=lastpostdesc" data-linktype="external"> Foro de MSDN </a>
            </li>
            <li>
                <a href="https://feedback.azure.com/forums/908035-sql-server" data-linktype="external"> UserVoice </a>
            </li>
        </ul>
    </div>