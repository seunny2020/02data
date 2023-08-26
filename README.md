# 02data
Streamlit App
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

# Set page configuration
st.set_page_config(
    page_title="Data Analysis Companion",
    page_icon=":bar_chart:",
    layout="wide"
)

# Navigation menu
menu = ["Home", "Our Services", "Reviews", "Sign Up"]
choice = st.sidebar.selectbox("Navigation", menu)

# Home Page
if choice == "Home":
    st.title("Welcome to Data Analysis Companion App")
    st.header("Upload a CSV or Excel File")
    
    # File upload
    uploaded_file = st.file_uploader("Choose a file", type=["csv", "xlsx"])
    
    # Display data overview if file is uploaded
    if uploaded_file is not None:
        st.subheader("Uploaded Data Overview")
        
        # Read the data into a pandas DataFrame
        data = pd.read_csv(uploaded_file)  # For CSV files
        # data = pd.read_excel(uploaded_file, engine='openpyxl')  # For Excel files
        
        # Display basic statistics
        st.write("Data Shape:", data.shape)
        st.write("Data Preview:")
        st.dataframe(data.head())
        
        # Generate histograms for numerical columns
        numeric_cols = data.select_dtypes(include=['float64', 'int64'])
        st.subheader("Data Visualizations")
        for col in numeric_cols.columns:
            st.write(f"## {col}")
            plt.hist(numeric_cols[col], bins='auto')
            st.pyplot(plt)

# Our Services Page
elif choice == "Our Services":
    st.title("Our Services")
    st.write("Discover the services we offer to help you with your data analysis needs.")
    # Add descriptions of your services here

# Reviews Page
elif choice == "Reviews":
    st.title("Customer Reviews")
    # Display customer reviews and testimonials
    # You can use st.write to add reviews or st.markdown for more formatting
    
    st.markdown("### John Doe")
    st.write("This app made data analysis a breeze. I'm a student and it helped me visualize my project data effortlessly!")
    
    st.markdown("### Jane Smith")
    st.write("The services provided are top-notch. I got valuable insights from my data that I wouldn't have discovered otherwise.")

# Sign Up Page
elif choice == "Sign Up":
    st.title("Sign Up for Updates")
    st.write("Subscribe to our newsletter to receive updates about new features and analysis tips.")
    
    # Sign-up form
    with st.form("signup_form"):
        email = st.text_input("Email:")
        name = st.text_input("Name:")
        submitted = st.form_submit_button("Sign Up")
        
        if submitted:
            st.success(f"Thank you, {name}! You're now subscribed to our newsletter with the email: {email}")
