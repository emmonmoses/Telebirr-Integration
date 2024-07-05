# Telebirr Integration Specification

This api provides interface specification for integration between CPS and Biller .

The target audience for this document includes: Solution Architect, Business Analyst, Developer, staff from design authority and technical department for business design, integration test and acceptance test teams from Telebirr and Appliedline.

# 1.0 C2BPaymentQueryRequest

When detecting a Query Bill transaction, the Mobile Money system sends a Query Bill request to the Biller system.

# 1.0.1 Request

The Mobile Money system sends a payment query request message to Biller system and waits for a response message.

# C2BPaymentQueryRequest (Code Snippet)

`<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Header/>
    <soapenv:Body>
        <c2b:C2BPaymentQueryRequest xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <TransType>11124</TransType>
            <TransID>{{$randomInt}}</TransID>
            <TransTime>20240301235900</TransTime>
            <BusinessShortCode>10069</BusinessShortCode>
            <BillRefNumber>I-D759C94BCE111</BillRefNumber>
            <MSISDN>251944111111</MSISDN>
        </c2b:C2BPaymentQueryRequest>
    </soapenv:Body>
</soapenv:Envelope>`

# 1.0.2 Response

After receiving the request, the third party replies with the response to Mobile Money system.

# C2BPaymentQueryResult (Code Snippet)

`<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <c2b:C2BPaymentQueryResult xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <ResultCode>0</ResultCode>
            <ResultDesc>OK</ResultDesc>
            <TransID>2</TransID>
            <BillRefNumber>I-859AB7CEF4</BillRefNumber>
            <UtilityName>Tuition Fee</UtilityName>
            <CustomerName>AAA BBB CCC</CustomerName>
            <Amount>12000.0000</Amount>
        </c2b:C2BPaymentQueryResult>
    </soapenv:Body>
</soapenv:Envelope>`

# 2.0 C2BPaymentValidationRequest

After internal verification is successful, the Mobile Money system submits Payment Validation request to the Biller system.

# 2.0.1 Request

The Mobile Money system sends a payment validation request message to Biller system and waits for a response message.

# C2BPaymentValidationRequest (Code Snippet)

`<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <c2b:C2BPaymentValidationRequest xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <TransType>PayBill</TransType>
            <TransID>{{$randomInt}}</TransID>
            <TransTime>20240301235920</TransTime>
            <TransAmount>12000</TransAmount>
            <BusinessShortCode>10069</BusinessShortCode>
            <BillRefNumber>I-D759C94BCE111</BillRefNumber>
            <InvoiceNumber></InvoiceNumber>
            <MSISDN>251944111111</MSISDN>
            <KYCInfo>
                <KYCName>FirstName</KYCName>
                <KYCValue>aaa</KYCValue>
            </KYCInfo>
            <KYCInfo>
                <KYCName>MiddleName</KYCName>
                <KYCValue>bbb</KYCValue>
            </KYCInfo>
            <KYCInfo>
                <KYCName>LastName</KYCName>
                <KYCValue>ccc</KYCValue>
            </KYCInfo>
        </c2b:C2BPaymentValidationRequest>
    </soapenv:Body>
</soapenv:Envelope>`

# 2.0.2 Response

After receiving the request, the third party replies with the response to Mobile Money system.

# C2BPaymentValidationResult (Code Snippet)

`<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <c2b:C2BPaymentValidationResult xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <ResultCode>0</ResultCode>
            <ResultDesc>Tuition Fee Processed</ResultDesc>
            <ThirdPartyTransID>R-JE0JSOG3BR</ThirdPartyTransID>
        </c2b:C2BPaymentValidationResult>
    </soapenv:Body>
</soapenv:Envelope>`

# 3.0 C2BPaymentConfirmationRequest

After the transaction is completed, the Mobile Money system sends a Payment Confirmation message to the the third-party system.

# 3.0.1 Request

The Mobile Money system sends a payment confirmation request message to third party and waits for a response message from third party.

# C2BPaymentConfirmationRequest (Code Snippet)

`<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <c2b:C2BPaymentConfirmationRequest xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <TransType>20032</TransType>
            <TransID>{{$randomInt}}</TransID>
            <TransTime>20240301235920</TransTime>
            <TransAmount>12000</TransAmount>
            <BusinessShortCode>10069</BusinessShortCode>
            <BillRefNumber>I-D759C94BCE111</BillRefNumber>
            <InvoiceNumber></InvoiceNumber>
            <ThirdPartyTransID>EACCI19014I-5A9044CB64</ThirdPartyTransID>
            <MSISDN>251944111111</MSISDN>
            <KYCInfo>
                <KYCName>FirstName</KYCName>
                <KYCValue>AAA</KYCValue>
            </KYCInfo>
            <KYCInfo>
                <KYCName>MiddleName</KYCName>
                <KYCValue>BBB</KYCValue>
            </KYCInfo>
            <KYCInfo>
                <KYCName>LastName</KYCName>
                <KYCValue>CCC</KYCValue>
            </KYCInfo>
        </c2b:C2BPaymentConfirmationRequest>
    </soapenv:Body>
</soapenv:Envelope>`

# 3.0.2 Response

After receiving the request, the third party replies with the response to Mobile Money system.

# C2BPaymentConfirmationResult (Code Snippet)

`<s<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
    <soapenv:Body>
        <c2b:C2BPaymentConfirmationResult xmlns:c2b="http://cps.huawei.com/cpsinterface/c2bpayment">
            <ResultCode>0</ResultCode>
            <ResultDesc>Tuition Fee Processed</ResultDesc>
        </c2b:C2BPaymentConfirmationResult>
    </soapenv:Body>
</soapenv:Envelope>`
