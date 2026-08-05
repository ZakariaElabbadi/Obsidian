if(
or(
and(
ISPICKVAL({stage}= "Close won"),
{amount} >= 50000
),
"⭐⭐ VIP Opportunity"
and(
ISPICKVAL({stage}= "Close won"),
{amount} < 50000
),
"✅ Standard Opportunity"

)