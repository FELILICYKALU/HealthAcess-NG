import streamlit as st
import pandas as pd
import plotly.express as px

# Load data
df = pd.read_excel("Imo_Healthcare_Data_With_Risk.xlsx")

st.set_page_config(page_title="Imo State Healthcare Dashboard", layout="wide")

st.title("🩺 Imo State Healthcare Dashboard")
st.markdown("Visualizing healthcare facility distribution and access gaps across LGAs.")

# Summary Metrics
st.subheader("Summary Statistics")
col1, col2, col3 = st.columns(3)
col1.metric("Total Facilities", f"{df['Facilities'].sum()}")
col2.metric("LGAs Covered", df['LGA'].nunique())
col3.metric("High-Risk LGAs", df[df['Risk_Level'] == 'High'].shape[0])

# Bar chart of facilities per LGA
st.subheader("📊 Healthcare Facilities by LGA")
bar_fig = px.bar(df, x="LGA", y="Facilities", color="Risk_Level", title="Facilities Distribution by LGA")
st.plotly_chart(bar_fig, use_container_width=True)

# Pie chart
st.subheader("📈 Risk Level Distribution")
pie_fig = px.pie(df, names="Risk_Level", title="Proportion of Risk Levels")
st.plotly_chart(pie_fig, use_container_width=True)

# Table view
st.subheader("📄 Raw Data")
st.dataframe(df)
