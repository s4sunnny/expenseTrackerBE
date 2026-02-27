# expenseTracker

<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="2.0" xmlns:exsl="http://exslt.org/common" exclude-result-prefixes="exsl">
  <xsl:variable name="colLooper">
    <xsl:call-template name="iterate">
      <xsl:with-param name="cbDataGroup" select="/Properties/Data/Group[@Name='Content block']"/>
      <xsl:with-param name="i" select="1"/>
      <xsl:with-param name="colCounter" select="0"/>
    </xsl:call-template>
  </xsl:variable>

<xsl:template name="render-content-block">
    <xsl:variable name="cbId" select="/Properties/Datum[@Name='Section Id']"/>
    <xsl:variable name="cbHeading" select="/Properties/Data/Group[@Name='Heading section']/Datum[@Name='Heading']"/>
    <xsl:variable name="cbIntroText" select="/Properties/Data/Group[@Name='Heading section']/Datum[@Name='Intro text']"/>
    <xsl:variable name="cbIntroOnly" select="/Properties/Data/Group[@Name='Heading section']/Datum[@Name='Intro only?']/Option[@Selected='true']/Value"/>
    <xsl:variable name="associateId" select="/Properties/Datum[@Name='Associate with tab by Tab ID (optional)']"/>
    <xsl:variable name="cbOverallOutroText" select="/Properties/Data/Group[@Name='Footer section']/Datum[@Name='Overall outro']"/>
    <xsl:variable name="colArray" select="exsl:node-set($colLooper)/colTotal" />
    <xsl:variable name="blockLayout" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Block Layout']/Option[@Selected='true']/Value" />
    <xsl:variable name="compType" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Component Type']/Option[@Selected='true']/Value" />
    <xsl:variable name="cardMargins" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Card Bottom Margin']/Option[@Selected='true']/Value" />
    <xsl:variable name="cardPaddingTop" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Card Padding top']/Option[@Selected='true']/Value" />
    <xsl:variable name="language" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Language Locale']/Option[@Selected='true']/Value" />
  <xsl:variable name="cardType" select="/Properties/Data/Group[@Name='Content section']/Datum[@Name='Card Type']/Option[@Selected='true']/Value" />

  <div class="cpc-component-outer clearfix">
  <div class="cpc-component">
    <xsl:attribute name="class"> 
     <xsl:if test="$compType != 'Content'"> cpc-component cpc-component-card <xsl:value-of select="$compType" /></xsl:if> 
   <xsl:if test="$cardMargins != 'No'"> card-margin</xsl:if>
   <xsl:if test="$cardType != 'card'"> cpc-component-card--tool</xsl:if> 
   <xsl:if test="$cardPaddingTop != 'Yes'"> cpc-component-card--no-padding</xsl:if> 
    </xsl:attribute>
   <div>
     <xsl:attribute name="class"><xsl:if test="$compType != 'white-bg'" >cpc-grid-container</xsl:if></xsl:attribute>
     <div class="cpc-cb cpc cpc-cb--col1">
    <xsl:if test="($cbHeading != '') or ($cbIntroText != '') "> 
        <div>
            <xsl:attribute name="class">cell<xsl:if test="$cbIntroOnly != 'Yes' "> cpc-cb__heading</xsl:if></xsl:attribute>
            <xsl:if test="$cbHeading != '' ">
                <h2 in-context-edit="{/Properties/Data/Group[@Name='Heading section']/Datum[@Name='Heading']/@ID}">
                       <xsl:if test="$cbId != ''">
                   <xsl:attribute name="id"><xsl:value-of select="$cbId"/></xsl:attribute>
              </xsl:if>
                  <xsl:value-of select="$cbHeading" disable-output-escaping="yes" />

              </h2>
            </xsl:if>

            <xsl:if test="$cbIntroText != '' ">
                <div in-context-edit="{/Properties/Data/Group[@Name='Heading section']/Datum[@Name='Intro text']/@ID}">
                  <xsl:value-of select="$cbIntroText" disable-output-escaping="yes" />
              </div>
            </xsl:if>
        </div>
    </xsl:if>
    </div>
      <div>
        <xsl:attribute name="class">cpc-cb cpc-cb--col<xsl:value-of select="$blockLayout" /></xsl:attribute>
        <xsl:for-each select="/Properties/Data/Group[@Name='Content block']">
          <xsl:variable name="cbColumnWidth" select="Datum[@Name='Column width']/Option[@Selected='true']/Value" /> 
          <xsl:variable name="cbOffset" select="Datum[@Name='Column offset']/Option[@Selected='true']/Value"/>
          <xsl:variable name="endClass">
            <xsl:if test="position() = last()"> end</xsl:if>
          </xsl:variable>
          <xsl:variable name="loopIndex" select="position()"/>
          <xsl:variable name="cbSubheading" select="Datum[@Name='Sub-heading']" />

          <xsl:variable name="cbSubheadingIDOLD" select="translate(concat($cbSubheading, '-', position()), ' ', '-')"   />
          <xsl:variable name="cbSubheadingsID" select="concat(Datum[@Name='Sub-heading']/@ID, $cbId)" />
          <xsl:variable name="cbBody" select="Datum[@Name='Body']" />

            <!-- image for content item -->
          <xsl:variable name="cbImagePath" select="Datum[@Name='Image']/Image/Path"/>
          <xsl:variable name="cbImageDescription" select="Datum[@Name='Image']/Image/Description"/> 
          <xsl:variable name="cbImageType" select="Datum[@Name='Image Type']/Option[@Selected='true']/Value" />
      <xsl:variable name="cbLoginIcon" select="Datum[@Name='login icon']/Option[@Selected='true']/Value" />
          <xsl:variable name="video-url" select="Datum[@Name='VideoUrl']" />
          <xsl:variable name="video-title" select="Datum[@Name='VideoTitle']" />
          <xsl:variable name="cbButtonText" select="Datum[@Name='Button Text']" />
          <xsl:variable name="cbButtonType" select="Datum[@Name='Button Type']/Option[@Selected='true']/Value" />
          <xsl:variable name="cbButtonLink" select="Datum[@Name='Button Link']" />
          <xsl:variable name="cbButtonCSSClass" select="Datum[@Name='Button CSS Classes']" />
          <xsl:variable name="cbModal" select="Datum[@Name='Sign in Modal (Optional)']/Option[@Selected='true']/Value" />           
          <xsl:variable name="cbAnalyticsID" select="Datum[@Name='Analytics ID (Optional)']/Option[@Selected='true']/Value" />
          <xsl:variable name="cbButton1Text" select="Datum[@Name='Button 1 Text']" />
          <xsl:variable name="cbButton1Type" select="Datum[@Name='Button 1 Type']/Option[@Selected='true']/Value" />
          <xsl:variable name="cbButton1Link" select="Datum[@Name='Button 1 Link']" />
          <xsl:variable name="cbModal1" select="Datum[@Name='Sign in Modal 1 (Optional)']/Option[@Selected='true']/Value" /> 
          <xsl:variable name="cbButton1CSSClass" select="Datum[@Name='Button 1 CSS Classes']" />
          <xsl:variable name="cbAnalyticsID1" select="Datum[@Name='Analytics 1 ID (Optional)']" />
          <xsl:variable name="cbCustomModal1" select="Datum[@Name='Custom Modal 1 ID (Optional)']"/>
          <xsl:variable name="cbCustomModalBody1" select="Datum[@Name='CTA Custom Modal Body 1 (Optional)']"/>
          <xsl:variable name="cbButton2Text" select="Datum[@Name='Button 2 Text']" />
          <xsl:variable name="cbButton2Type" select="Datum[@Name='Button 2 Type']/Option[@Selected='true']/Value" />
          <xsl:variable name="cbButton2Link" select="Datum[@Name='Button 2 Link']" />
          <xsl:variable name="cbModal2" select="Datum[@Name='Sign in Modal 2 (Optional)']/Option[@Selected='true']/Value" /> 
          <xsl:variable name="cbButton2CSSClass" select="Datum[@Name='Button 2 CSS Classes']" />
          <xsl:variable name="cbAnalyticsID2" select="Datum[@Name='Analytics 2 ID (Optional)']" />
          <xsl:variable name="cbCustomModal2" select="Datum[@Name='Custom Modal 2 ID (Optional)']"/>
          <xsl:variable name="cbCustomModalBody2" select="Datum[@Name='CTA Custom Modal Body 2 (Optional)']"/>
          <xsl:variable name="cbButton3Text" select="Datum[@Name='Button 3 Text']" />
          <xsl:variable name="cbButton3Type" select="Datum[@Name='Button 3 Type']/Option[@Selected='true']/Value" />
          <xsl:variable name="cbButton3Link" select="Datum[@Name='Button 3 Link']" />
          <xsl:variable name="cbModal3" select="Datum[@Name='Sign in Modal 3 (Optional)']/Option[@Selected='true']/Value" /> 
          <xsl:variable name="cbButton3CSSClass" select="Datum[@Name='Button 3 CSS Classes']" />
          <xsl:variable name="cbAnalyticsID3" select="Datum[@Name='Analytics 3 ID (Optional)']" />
          <xsl:variable name="cbCustomModal3" select="Datum[@Name='Custom Modal 3 ID (Optional)']"/>
          <xsl:variable name="cbCustomModalBody3" select="Datum[@Name='CTA Custom Modal Body 3 (Optional)']"/>
          <xsl:variable name="cbOutro" select="Datum[@Name='Outro']" />

          <xsl:if test="($cbBody != '') or ($cbSubheading != '')">
            <div>
               <xsl:attribute name="class">cell cpc-cb__content<xsl:if test="$blockLayout = 'feature' and (string-length($cbImagePath) > 1) and ($cbImagePath != '$URL_PREFIX/assets/cpc/uploads/')" > grid-x align-center</xsl:if> 
                 <xsl:if test="($cbButton1Text != '' or $cbButton2Text != '' or $cbButton3Text != '')"> no-link</xsl:if>
                 <xsl:if test="$compType != 'Content'"> cpc-cb__content__card cpc-cb__content__card--<xsl:value-of select="$compType" /></xsl:if> 
              </xsl:attribute>

              <xsl:choose>
                <xsl:when test="$video-url != ''">
                  <div class="cell cpc-video-player">
                    <button class="video-button" style="background-image: url({$cbImagePath});">
                      <xsl:attribute name="aria-label">Video play <xsl:value-of select="$video-title"/></xsl:attribute>
                    </button>
                    <iframe class="videoIframe" tabindex="-1" src="" frameborder="0"
                            data-src="{$video-url}" allow="autoplay; fullscreen"
                            allowtransparency="true">
                      <xsl:attribute name="title"><xsl:value-of select="$video-title"/></xsl:attribute>
                    </iframe>
                  </div>
                </xsl:when>
                <xsl:otherwise> 
                  <xsl:if test="(string-length($cbImagePath) > 1) and ($cbImagePath != '$URL_PREFIX/assets/cpc/uploads/') ">
                    <img>   
                      <xsl:attribute name="src"><xsl:value-of select="$cbImagePath"/></xsl:attribute>
                      <xsl:attribute name="class">cpc-cb__image cpc-cb__image--<xsl:value-of select="$cbImageType"/>
                        <xsl:if test="$cbImageType = 'logo' and $cbButton1Type = 'link'"> cpc-cb__logoLinks</xsl:if> 
                      </xsl:attribute>
                      <xsl:attribute name="title"><xsl:value-of select="$cbImageDescription"/></xsl:attribute>
                      <xsl:attribute name="alt"><xsl:value-of select="$cbImageDescription"/></xsl:attribute>
                    </img>
                  </xsl:if>        

                </xsl:otherwise>
              </xsl:choose>

              <xsl:choose>
                <xsl:when test="($cbSubheading != '') and ($cbHeading != '')">
                  <h3 in-context-edit="{Datum[@Name='Sub-heading']/@ID}">
                    <xsl:attribute name="class">cpc-cb__sub-heading</xsl:attribute>
                    <xsl:attribute name="id"><xsl:value-of select="$cbSubheadingsID" disable-output-escaping="yes"/></xsl:attribute>
                    <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" />

                  </h3>
                  <xsl:if test="$cbLoginIcon != 'select icon'">
                    <img>   
                      <xsl:attribute name="src">/cpc/assets/cpc/uploads/icons/<xsl:value-of select="$cbLoginIcon"/>.svg</xsl:attribute>
                      <xsl:attribute name="class">cpc-cb__image cpc-cb__image--<xsl:value-of select="$cbLoginIcon"/></xsl:attribute> 
                      <xsl:choose>
                        <xsl:when test="$language = 'fr'">
                          <xsl:if test="$cbLoginIcon = 'login-icon'">
                            <xsl:attribute name="aria-label">Vous devez ouvrir une session pour utiliser le service de <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" /></xsl:attribute>
                            </xsl:if> 
                          <xsl:if test="$cbLoginIcon = 'logout-icon'">
                           <xsl:attribute name="alt"></xsl:attribute>
                          </xsl:if> 
            </xsl:when>
                        <xsl:otherwise>
                          <xsl:if test="$cbLoginIcon = 'login-icon'">
                             <xsl:attribute name="aria-label">You must be signed in to use <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" /></xsl:attribute>
                          </xsl:if> 
                          <xsl:if test="$cbLoginIcon = 'logout-icon'">
                              <xsl:attribute name="alt"></xsl:attribute>
                          </xsl:if> 
            </xsl:otherwise>
                      </xsl:choose>

                    </img>
                  </xsl:if>
                </xsl:when>
                <xsl:when test="$cbSubheading != '' ">
                  <h2 in-context-edit="{Datum[@Name='Sub-heading']/@ID}">
                    <xsl:attribute name="class">cpc-cb__sub-heading</xsl:attribute>
                    <xsl:attribute name="id"><xsl:value-of select="$cbSubheadingsID" disable-output-escaping="yes"/></xsl:attribute>
                    <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" />
                  </h2>
                </xsl:when>
              </xsl:choose>

              <xsl:choose>
                <xsl:when test="$cbBody != '' "> 
                  <div in-context-edit="{Datum[@Name='Body']/@ID}">
                      <xsl:if test="$cbImageType != 'custom'"><xsl:attribute name="class">cpc-cb__text</xsl:attribute></xsl:if>
                    <xsl:value-of select="$cbBody" disable-output-escaping="yes" />
                  </div>
                </xsl:when>
              </xsl:choose>

        <xsl:choose>
          <xsl:when test="$cbButton1Text != '' or $cbButton2Text != '' or $cbButton3Text != '' "> 
            <div>
              <xsl:if test="(($cbButton1Text !='' and $cbButton1Type != 'link') or ($cbButton2Text !='' and $cbButton2Type != 'link') or ($cbButton3Text !='' and $cbButton3Type != 'link'))">
                <xsl:attribute name="class">cpc-cb__cta</xsl:attribute>
              </xsl:if>
              <xsl:if test="$cbButton1Text != '' ">
                <xsl:choose>
                  <xsl:when test="$cbButton1Type = 'link'">
                    <a role="link" in-context-edit="{Datum[@Name='Button 1 Text']/@ID}">
                      <xsl:choose>
                        <xsl:when test="$cbButton1CSSClass != '' ">
                          <xsl:attribute name="class"><xsl:value-of select="$cbButton1CSSClass"/></xsl:attribute>    
                        </xsl:when>
                        <xsl:otherwise> 
                          <xsl:attribute name="class">standalone</xsl:attribute>  
                        </xsl:otherwise>                    
                      </xsl:choose>
                        <xsl:choose>
                          <xsl:when test="$cbAnalyticsID1 != '' ">
                            <xsl:attribute name="id"><xsl:value-of select="$cbAnalyticsID1"/></xsl:attribute>
                          </xsl:when>
                        </xsl:choose>
                        <xsl:attribute name="href"><xsl:value-of select="$cbButton1Link"/></xsl:attribute>

                <xsl:if test="$cardType != 'card'"> 
                              <xsl:choose>
                                <xsl:when test="$language = 'fr'">
                                  <xsl:attribute name="aria-label">Utiliser l'outil maintenant - <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" /></xsl:attribute>
                                  </xsl:when>
                                  <xsl:otherwise>
                                   <xsl:attribute name="aria-label">Use tool now - <xsl:value-of select="$cbSubheading" disable-output-escaping="yes" /></xsl:attribute>
                                  </xsl:otherwise>
                                </xsl:choose>
                     </xsl:if>
                              <xsl:if test="$cbModal1 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal1"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton1Text" disable-output-escaping="yes" />
                           </a>
                          </xsl:when>
                       <xsl:otherwise>
                          <button in-context-edit="{Datum[@Name='Button 1 Text']/@ID}">
                            <xsl:choose>
                              <xsl:when test="$cbAnalyticsID1 != '' ">
                                <xsl:attribute name="ID"><xsl:value-of select="$cbAnalyticsID1"/></xsl:attribute>
                              </xsl:when>
                            </xsl:choose>
                            <xsl:attribute name="href"><xsl:value-of select="$cbButton1Link"/></xsl:attribute>
                            <xsl:attribute name="class">  
                              <xsl:value-of select="$cbButton1Type"/>
                              <xsl:if test="string-length($cbButton1CSSClass) > 0">
                              <xsl:value-of select="concat(' ', $cbButton1CSSClass)"/>
                              </xsl:if>
                            </xsl:attribute>
                            <xsl:if test="$cbModal1 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal1"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton1Text" disable-output-escaping="yes" />
                          </button>
                         </xsl:otherwise>
                   </xsl:choose>

                  </xsl:if>

                  <xsl:if test="$cbButton2Text != '' ">
             <xsl:choose>
                         <xsl:when test="$cbButton2Type = 'link'">
                           <a role="link" in-context-edit="{Datum[@Name='Button 2 Text']/@ID}">
                              <xsl:choose>
                                <xsl:when test="$cbButton2CSSClass != '' ">
                                    <xsl:attribute name="class"><xsl:value-of select="$cbButton2CSSClass"/></xsl:attribute>    
                                </xsl:when>
                                  <xsl:otherwise> 
                                     <xsl:attribute name="class">standalone</xsl:attribute>  
                                 </xsl:otherwise>                    
                              </xsl:choose>
                              <xsl:choose>
                                <xsl:when test="$cbAnalyticsID2 != '' ">
                                  <xsl:attribute name="id"><xsl:value-of select="$cbAnalyticsID2"/></xsl:attribute>
                                </xsl:when>
                              </xsl:choose>
                            <xsl:attribute name="href"><xsl:value-of select="$cbButton2Link"/></xsl:attribute>
                              <xsl:if test="$cbModal2 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal2"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton2Text" disable-output-escaping="yes" />
                           </a>
                          </xsl:when>
                       <xsl:otherwise>
                          <button in-context-edit="{Datum[@Name='Button 2 Text']/@ID}">
                            <xsl:choose>
                              <xsl:when test="$cbAnalyticsID2 != '' ">
                                <xsl:attribute name="id"><xsl:value-of select="$cbAnalyticsID2"/></xsl:attribute>
                              </xsl:when>
                            </xsl:choose>
                            <xsl:attribute name="href"><xsl:value-of select="$cbButton2Link"/></xsl:attribute>
                            <xsl:attribute name="class">
                              <xsl:value-of select="$cbButton2Type"/>
                              <xsl:if test="string-length($cbButton2CSSClass) > 0">
                              <xsl:value-of select="concat(' ', $cbButton2CSSClass)"/>
                              </xsl:if>
                            </xsl:attribute>
                            <xsl:if test="$cbModal2 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal2"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton2Text" disable-output-escaping="yes" />
                          </button>
                         </xsl:otherwise>
                   </xsl:choose>

                  </xsl:if>
                   <xsl:if test="$cbButton3Text != '' ">
             <xsl:choose>
                         <xsl:when test="$cbButton3Type = 'link'">
                           <a role="button" in-context-edit="{Datum[@Name='Button 3 Text']/@ID}">
                             <xsl:choose>
                                <xsl:when test="$cbButton3CSSClass != '' ">
                                    <xsl:attribute name="class"><xsl:value-of select="$cbButton3CSSClass"/></xsl:attribute>    
                                </xsl:when>
                                <xsl:otherwise> 
                                     <xsl:attribute name="class">standalone</xsl:attribute>  
                                 </xsl:otherwise>                    
                          </xsl:choose>
                            <xsl:choose>
                              <xsl:when test="$cbAnalyticsID3 != '' ">
                                <xsl:attribute name="ID"><xsl:value-of select="$cbAnalyticsID3"/></xsl:attribute>
                              </xsl:when>
                            </xsl:choose>
                            <xsl:attribute name="href"><xsl:value-of select="$cbButton3Link"/></xsl:attribute>
                              <xsl:if test="$cbModal3 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal3"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton3Text" disable-output-escaping="yes" />
                           </a>
                          </xsl:when>
                       <xsl:otherwise>
                          <button in-context-edit="{Datum[@Name='Button 3 Text']/@ID}">
                            <xsl:choose>
                              <xsl:when test="$cbAnalyticsID3 != '' ">
                                <xsl:attribute name="ID"><xsl:value-of select="$cbAnalyticsID3"/></xsl:attribute>
                              </xsl:when>
                            </xsl:choose>
                            <xsl:attribute name="href"><xsl:value-of select="$cbButton3Link"/></xsl:attribute>
                            <xsl:attribute name="class">
                               <xsl:value-of select="$cbButton3Type"/>
                              <xsl:if test="string-length($cbButton3CSSClass) > 0">
                              <xsl:value-of select="concat(' ', $cbButton3CSSClass)"/>
                              </xsl:if>
                            </xsl:attribute>
                            <xsl:if test="$cbModal3 != ''">
                            <xsl:attribute name="data-cpc-modal-secure-cta"><xsl:value-of select="$cbModal3"/></xsl:attribute>
                            </xsl:if>                  
                            <xsl:value-of select="$cbButton3Text" disable-output-escaping="yes" />
                          </button>
                         </xsl:otherwise>
                   </xsl:choose>
                  </xsl:if>
            </div>
          </xsl:when>
          <xsl:otherwise>
            <div style="display:none;"></div>
          </xsl:otherwise>
        </xsl:choose>    

            </div>

            </xsl:if>

            <xsl:if test="$cbOutro != ''">
                <div class="cpc-cb__outro">
                  <div in-context-edit="{Datum[@Name='Outro']/@ID}"><xsl:value-of select="$cbOutro" disable-output-escaping="yes" /></div>                     
              </div>
            </xsl:if>

            <xsl:if test="$cbCustomModalBody1 != '' ">
              <xsl:value-of select="$cbCustomModalBody1" disable-output-escaping="yes" />
            </xsl:if>

            <xsl:if test="$cbCustomModalBody2 != '' ">
              <xsl:value-of select="$cbCustomModalBody2" disable-output-escaping="yes" />
            </xsl:if>

            <xsl:if test="$cbCustomModalBody3 != '' ">
              <xsl:value-of select="$cbCustomModalBody3" disable-output-escaping="yes" />
            </xsl:if>

        </xsl:for-each>
    </div> 
  </div> 
  </div> 
  </div> 


  </xsl:template>
  <xsl:template name="iterate">
    <xsl:param name="cbDataGroup"/>
    <xsl:param name="i" />
    <xsl:param name="colCounter"/>
    <xsl:param name="videoCounter" select="0"/>
   <xsl:value-of select="$colCounter" disable-output-escaping="yes" />
    <xsl:choose>
      <xsl:when test="($colCounter > 4)">
        <colTotal>true</colTotal>
      </xsl:when>
      <xsl:otherwise>
        <colTotal>false</colTotal>
      </xsl:otherwise>
    </xsl:choose>

    <xsl:if test="count($cbDataGroup) > $i">
      <xsl:call-template name="iterate">
        <xsl:with-param name="cbDataGroup" select="$cbDataGroup"/>
        <xsl:with-param name="i" select="$i + 1"/>
        <xsl:with-param name="colCounter" select="$colCounter"/>

      </xsl:call-template>
    </xsl:if>
  </xsl:template>    
</xsl:stylesheet>
