# Tax-Rounding-off
hello am using unicenta pos in a restaurant and i want my taxes to be rounded off to 2 decimal places but the code am using the result is a long figure.check out the code and advice.
<?xml version="1.0" encoding="UTF-8"?>
<!-- 
    uniCenta oPOS - Touch friendly Point Of Sale
    Copyright (c) 2009-2017 uniCenta.
    http://sourceforge.net/projects/unicentaopos

    This file is part of uniCenta oPOS.

    uniCenta oPOS is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    uniCenta oPOS is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with uniCenta oPOS.  If not, see <http://www.gnu.org/licenses/>.
 -->

<output>

    <display>
        <line><text align="left" length="8">Total</text><text align="right" length="12">${ticket.printTotal()}</text></line>
        <line><text align="center" length="20">Thank you</text></line>
    </display>

 

    <ticket>
        <image>Printer.Ticket.Logo</image>
        <line>
        </line>
  
        <line>
            <text align="center" length="42" bold="true">A. </text>
        </line>
    <line>
            <text align="center" length="42" bold="true">P.O BOX 1033-80109 MTWAPA</text>
        </line>

    <line>
            <text align="center" length="42" bold="true">EMAIL:ARCASAURINA@GMAIL.COM

 </text>
        </line>
<line>
            <text align="center" length="42" bold="true">TEL:0713918920 </text>
        </line>
<line>
            <text align="center" length="42" bold="true">PIN:P051769574F </text>
        </line>
<line>
            <text align="center" length="42" bold="true">CUSTOMER BILL  </text>
        </line>
        <line></line>

	#if (${ticket.ticketType} == 0)
            <line>
                <text align="left" length="15">Receipt:</text>
                <text>${ticket.printId()}</text>
            </line>
	#end

	#if (${ticket.ticketType} == 1)
            <line>
                <text align="left" length="15">Refund:</text>
                <text>${ticket.printId()}</text>
            </line>
	#end
	
        <line>
            <text align="left" length="15">Date:</text>
            <text>${ticket.printDate()}</text>
        </line>
        <line>
            <text align="left" length="15">Terminal: </text>
            <text>${ticket.getHost()}</text>
        </line> 
        <line>
            <text align="left" length="15">Served by:</text>
            <text>${ticket.printUser()}</text>
        </line>

	#if ($ticket.getCustomer())
            <line>
                <text align="left" length="15">Account #:</text>
                <text>${ticket.getCustomer().printTaxCustomerID()}</text>
            </line>
            <line>
                <text align="left" length="15">Customer:</text>
                <text>${ticket.getCustomer().printName()}</text>
            </line>
            <line>
                <text align="left" length="15">Address:</text>
                <text>${ticket.getCustomer().printAddress()}</text>
            </line>
            <line>
                <text align="left" length="15">Postal:</text>
                <text>${ticket.getCustomer().printPostal()}</text>
            </line>
            <line>
                <text align="left" length="15">Phone:</text>
                <text>${ticket.getCustomer().printPhone()}</text>
            </line>
            <line>
                <text align="left" length="15">Current Debt:</text>
                <text>${ticket.getCustomer().printCurDebt()}</text>
            </line>
<!-- 	    <line><barcode type="CODE128">${ticket.getCustomer().printTaxCustomerID()}</barcode></line>                 -->
	#end     

	#if (${tickettext.place} != ${place})
            <line>
                <text align="left" length="15">Table:</text>
                <text>${place}</text>
            </line>
	#end
	<line></line>

        <line>
            <text align ="left" length="17">Item</text>
            <text align ="right" length="8">Price</text>
            <text align ="right" length="7">Qty</text>
            <text align ="right" length="10">Value</text>
        </line>
	<line>
            <text align="left" length="42">------------------------------------------</text>
        </line>
    
        #foreach ($ticketline in $ticket.getLines())
        <line>
            #if ($ticketline.isProductCom())
		<text align ="left" length="17">*${ticketline.printName()}</text>
            #else
		<text align ="left" length="17">${ticketline.printName()}</text>
            #end
            <text align ="right" length="8">${ticketline.printPriceTax()}</text>
            <text align ="right" length="7">x${ticketline.printMultiply()}</text>
            <text align ="right" length="10">${ticketline.printValue()}</text>
        </line>
        
<!-- un-comment line below if you want to add a product's properties -->
            <!-- <line><text align ="left" length="42">${ticketline.getProperty("ingredients", "")}</text> </line> -->

<!-- un-comment line below if you want to add a user input sales line's Note -->
            <!-- <line><text align ="left" length="42">${ticketline.getProperty("notes", "")}</text> </line> -->              

            #if ($ticketline.productAttSetInstId)
                <line>
                    <text align ="left" length="42">${ticketline.productAttSetInstDesc}</text>
                </line>
            #end
        #end

        <line>
            <text align="left" length="42">------------------------------------------</text>
        </line>
	<line>
            <text>Items count: </text>
            <text align ="left" length="14">${ticket.printArticlesCount()}</text>
        </line>
	<line></line>
	<line size="1">
            <text align ="left" length="18" bold="true">Total without VAT</text>
            <text align ="right" length="26" bold="true">${ticket.printTotal()}</text>
        </line>
    
#set ($VAT =  ${ticket.getTotal()} /1.16 * 16/100)
#set ($LEVY =  ${ticket.getTotal()} /1.18 * 2/100)
#set ($SCHARGE =  ${ticket.getTotal()} /1.18 * 5/100)
#set ($AMTPLUSVAT =  ${ticket.getTotal()} +$VAT)
    var taxAmtRnd = Math.round(taxAmount*100);
             taxAmtRnd = taxAmtRnd/100; 
          
    }
            else if (VatRate > 0) VatAmount = (Price * VatRate) / 100;
            else VatAmount = 0;
            var taxAmtRnd = Math.round(taxAmount*100);
            taxAmtRnd = taxAmtRnd/100; 
          
            
          
   
        <line></line>
<line><text align="center" length="42" bold="true">TOTAL WITH VAT INCL: ${ticket.getTotal()}  </text></line>
<line><text align="center" length="42" bold="true">16% VAT AMOUNT : $VAT</text></line>

<line><text align="center" length="42" bold="true">2% CATERING LEVY AMOUNT : $LEVY</text></line>

        <line></line>
       

        #foreach ($paymentline in $ticket.payments)
            #if ($paymentline.name == "cash")
            <line>
                <text bold="true">Cash</text>
            </line>
            <line>
                <text align="left" length="22">Tendered:</text>
                <text align ="right" length="20">${paymentline.printPaid()}</text>
            </line>
            <line>
                <text align="left" length="22">Change:</text>
                <text align ="right" length="20">${paymentline.printChange()}</text>
            </line>
            #end
          	
            #if ($paymentline.name == "cashrefund")
            <line>
                <text align="left" length="22" bold="true">Refund</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
            #if ($paymentline.name == "cheque")
            <line>
                <text align="left" length="22" bold="true">Cheque</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
            #if ($paymentline.name == "chequerefund")
            <line>
                <text align="left" length="22" bold="true">Cheque Refund</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>                
            </line>
            #end
            #if ($paymentline.name == "voucherin")
            <line>
                <text align="left" length="22" bold="true">Voucher</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
            #if ($paymentline.name == "voucherout")
            <line>
                <text align="left" length="22" bold="true">Note Refund</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
            #if ($paymentline.name == "slip")
            <line>
                <text align="left" length="22" bold="true">Slip</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
            #if ($paymentline.name == "free")
            <line>
                <text align="left" length="22" bold="true">Free</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
	    #if ($paymentline.name == "debt")
            <line>
                <text align="left" length="22" bold="true">On Account</text>
                <text align ="right" length="20">${paymentline.printTotal()}</text>
            </line>
            #end
        #end
 
            <line></line>


#set ($VAT =  ${ticket.getTotal()} /1.18 * 16/100)
#set ($LEVY =  ${ticket.getTotal()} /1.18 * 2/100)
#set ($SCHARGE =  ${ticket.getTotal()} /1.18 * 5/100)
  var taxAmtRnd = Math.round(taxAmount*100);
             taxAmtRnd = taxAmtRnd/100; 
        <line></line>
<line><text align="center" length="42" bold="true">TOTAL AMT: ${ticket.getTotal()} </text></line>
<line><text align="center" length="42" bold="true">16% VAT AMOUNT : $VAT</text></line>

<line><text align="center" length="42" bold="true">2% CATERING LEVY AMOUNT : $LEVY</text></line>


        #foreach ($ticketline in $ticket.getLines())
 
            #if ($ticketline.productAttSetInstId)
                 <line><text align="center" length="42" bold="true">5% SERVICE CHARGE : $SCHARGE</text></line>
        
       #end
#end

 
            <line></line>
        <line>
            <text align="center" length="42" bold="true" > PRICES INCLUSIVE OF ALL TAXES</text>
        </line>  
        <line>
            <text bold="true">==========================================</text>
        </line>
        

        <line>
            <text align="center" length="42" bold="true" >KARIBU TENA </text>
        </line>  
        <line>
            <text bold="true">==========================================</text>
        </line>
        























        <line>
            <text align="center" length="42" bold="true" >SOFTWARE INSTALLED BY 0706505232. </text>
        </line>  
        <line></line>

        #foreach ($paymentline in $ticket.payments)
            #if ($paymentline.name == "magcard")
                #if ($paymentline.chipAndPin)
                <line size="1">
                    <text align="center" length="42" bold="true">CARD SALE</text>
                </line>
                <line size="1">
                    <text>${paymentline.getCardName()}</text>
                </line>
                <line>
                    <text>${paymentline.printCardNumber()}</text>
                </line>
                <line></line>
                <line size="1">
                    <text align="left" length="10">AMOUNT</text>
                    <text align ="right" length="32">${paymentline.printTotal()}</text></line>
                <line>
                    <text>Tranx ID    : </text>
                    <text>${paymentline.printTransactionID()}</text>
                </line>
                <line>
                    <text>Auth Code   : </text>
                    <text>${paymentline.printAuthorization()}</text>
                </line>
                <line>
                    <text>Verified By : </text>
                    <text>${paymentline.printVerification()}</text>
                </line>
                #end
                #if (!$paymentline.chipAndPin)
                <line size="1">
                    <text align="center" length="42" bold="true">CARD SALE</text>
                </line>
                <line size="1">
                    <text>${paymentline.getCardName()}</text>
                </line>    
                <line>
                    <text>${paymentline.printCardNumber()}</text>
                </line>
                <line></line>
                <line size="1">
                    <text align="left" length="10">AMOUNT</text>
                <text align ="right" length="32">${ticket.printTotal()}</text></line>
                <line>
                    <text align ="left" length="22">Expiration Date:</text>
                    <text>${paymentline.printExpirationDate()}</text>
                </line>
                <line>
                   <text>Operation : </text>
                   <text>${paymentline.printTransactionID()}</text>
                </line>
                <line>
                    <text>Auth Code : </text>
                    <text>${paymentline.printAuthorization()}</text>
                </line>
                <line></line>
                #end
                #if ($ticket.hasTip())
                <line>
                    <text align ="left" length="16">Tip:</text>
                    <text align ="right" length="26">_______________</text></line>
                <line></line>
        
                <line size="1">
                    <text align ="left" length="16" bold="false">Total</text>
                    <text align ="right" length="26" bold="false">_______________</text></line>
                <line></line>
                <line></line>
                <line size="1">
                    <text align ="left" length="42" bold="false">__________________________________________</text>
                </line>
                <line size="1">
                    <text align ="center" length="42" bold="false">Signature</text>
                </line>
                #else
                <line size="1">
                    <text align ="left" length="16" bold="true">Total</text>
                    <text align ="right" length="26" bold="true">${ticket.printTotal()}</text>
                </line>
                #end            
            #end
        #if ($paymentline.name == "magcardrefund")
            <line size="1">
                <text align="center" length="42" bold="true">CARD REFUND</text>
            </line>
            <line size="1">
                <text>${paymentline.getCardName()}</text>
            </line>    
            <line>
                <text>${paymentline.printCardNumber()}</text>
            </line>
            <line></line>
            <line size="1">
                <text align="left" length="10">AMOUNT</text>
                <text align ="right" length="32">${paymentline.printTotal()}</text></line>
            <line>
                <text align ="left" length="22">Expiration Date:</text>
                <text>${paymentline.printExpirationDate()}</text></line>
            <line>
                <text>Tranx ID  : </text>
                <text>${paymentline.printTransactionID()}</text>
            </line>
            <line>
                <text>Auth Code : </text>
                <text>${paymentline.printAuthorization()}</text>
            </line>
            <line></line>                
        #end
    #end

</ticket>


#foreach ($paymentline in $ticket.payments)
#if ($paymentline.name == "cash")
    <opendrawer/>
#end
    #if ($paymentline.name == "cashrefund")
            <opendrawer/>
    #end
#end

</output>
