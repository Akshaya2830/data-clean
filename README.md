# data-clean
import pandas as pd
import numpy as np
from sklearn.preprocessing import MinMaxScaler
df = pd.DataFrame({
&#39;Date&#39;: [&#39;2023-01-01&#39;, &#39;02-01-2023&#39;, &#39;Invalid&#39;],
&#39;Category&#39;: [&#39;Apple&#39;, &#39;apple&#39;, &#39;Banana&#39;],
&#39;Value&#39;: [10, 1500, 20],
&#39;Missing&#39;: [1, np.nan, 3]
})
print(&quot;Original Data:\n&quot;, df)
df.drop_duplicates(inplace=True)
df[&#39;Missing&#39;].fillna(df[&#39;Missing&#39;].mean(), inplace=True)
df[&#39;Date&#39;] = pd.to_datetime(df[&#39;Date&#39;], errors=&#39;coerce&#39;).fillna(method=&#39;ffill&#39;)
df[&#39;Category&#39;] = df[&#39;Category&#39;].str.lower()
df[&#39;Value&#39;] = np.where(df[&#39;Value&#39;] &gt; 100, 100, df[&#39;Value&#39;])
scaler = MinMaxScaler()
df[&#39;Value_norm&#39;] = scaler.fit_transform(df[[&#39;Value&#39;]])
print(&quot;\nCleaned Data:\n&quot;, df)
