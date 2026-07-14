import os
import tempfile
import streamlit as st
from shopping_agent import agent
 
# ---------------------------------------------------------------------------
# Custom CSS Styling
# ---------------------------------------------------------------------------
st.markdown("""
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
 
    /* Main background */
    [data-testid="stAppViewContainer"] {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        min-height: 100vh;
    }
 
    [data-testid="stSidebarContent"] {
        background: linear-gradient(180deg, #1a1a2e 0%, #16213e 100%);
    }
 
    /* Header Styling */
    .header-container {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        padding: 40px 20px;
        border-radius: 20px;
        margin-bottom: 30px;
        box-shadow: 0 8px 32px rgba(102, 126, 234, 0.4);
        animation: slideDown 0.6s ease-out;
    }
 
    @keyframes slideDown {
        from {
            opacity: 0;
            transform: translateY(-30px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
 
    .header-title {
        font-size: 3em;
        font-weight: 800;
        color: white;
        text-align: center;
        margin-bottom: 10px;
        text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
    }
 
    .header-caption {
        font-size: 1.1em;
        color: #e0e0ff;
        text-align: center;
        font-weight: 500;
    }
 
    /* Sidebar Upload Card */
    .upload-card {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        padding: 25px;
        border-radius: 15px;
        margin: 20px 0;
        box-shadow: 0 8px 24px rgba(102, 126, 234, 0.3);
        border: 2px solid rgba(255, 255, 255, 0.1);
    }
 
    .upload-card h3 {
        color: white;
        margin-bottom: 10px;
        font-size: 1.3em;
    }
 
    .upload-card p {
        color: #e0e0ff;
        font-size: 0.9em;
        margin-bottom: 15px;
    }
 
    /* Chat Bubbles */
    .user-message {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        color: white;
        padding: 15px 20px;
        border-radius: 18px;
        margin: 10px 0;
        max-width: 70%;
        margin-left: auto;
        box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        border-bottom-right-radius: 4px;
        animation: slideInRight 0.3s ease-out;
    }
 
    .assistant-message {
        background: white;
        color: #1a1a2e;
        padding: 15px 20px;
        border-radius: 18px;
        margin: 10px 0;
        max-width: 70%;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        border-bottom-left-radius: 4px;
        animation: slideInLeft 0.3s ease-out;
    }
 
    @keyframes slideInRight {
        from {
            opacity: 0;
            transform: translateX(30px);
        }
        to {
            opacity: 1;
            transform: translateX(0);
        }
    }
 
    @keyframes slideInLeft {
        from {
            opacity: 0;
            transform: translateX(-30px);
        }
        to {
            opacity: 1;
            transform: translateX(0);
        }
    }
 
    /* Input Field */
    .stChatInput input {
        background: white !important;
        border: 2px solid #667eea !important;
        border-radius: 25px !important;
        padding: 12px 20px !important;
        font-size: 1em !important;
        color: #1a1a2e !important;
    }
 
    .stChatInput input:focus {
        border-color: #764ba2 !important;
        box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1) !important;
    }
 
    /* Buttons */
    .stButton > button {
        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
        color: white !important;
        border: none !important;
        border-radius: 12px !important;
        padding: 12px 24px !important;
        font-weight: 600 !important;
        font-size: 1em !important;
        transition: all 0.3s ease !important;
        box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3) !important;
    }
 
    .stButton > button:hover {
        transform: translateY(-2px) !important;
        box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4) !important;
    }
 
    .stButton > button:active {
        transform: translateY(0) !important;
    }
 
    /* Loading Spinner */
    .spinner-container {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 20px;
    }
 
    .spinner {
        width: 50px;
        height: 50px;
        border: 4px solid rgba(102, 126, 234, 0.2);
        border-top-color: #667eea;
        border-radius: 50%;
        animation: spin 0.8s linear infinite;
    }
 
    @keyframes spin {
        to { transform: rotate(360deg); }
    }
 
    /* Product Card */
    .product-card {
        background: white;
        border-radius: 15px;
        padding: 20px;
        margin: 15px 0;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        border-left: 5px solid #667eea;
        transition: all 0.3s ease;
    }
 
    .product-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
    }
 
    /* Success Message */
    .success-message {
        background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
        color: white;
        padding: 15px 20px;
        border-radius: 12px;
        margin: 10px 0;
        box-shadow: 0 4px 15px rgba(17, 153, 142, 0.3);
    }
 
    /* Error Message */
    .error-message {
        background: linear-gradient(135deg, #eb3349 0%, #f45c43 100%);
        color: white;
        padding: 15px 20px;
        border-radius: 12px;
        margin: 10px 0;
        box-shadow: 0 4px 15px rgba(235, 51, 73, 0.3);
    }
 
    /* Sidebar styling */
    .sidebar-header {
        color: white;
        font-size: 1.5em;
        font-weight: 700;
        margin-bottom: 10px;
        text-align: center;
    }
 
    .sidebar-caption {
        color: #b0b0ff;
        text-align: center;
        font-size: 0.9em;
        margin-bottom: 20px;
    }
 
    /* Footer */
    .footer {
        background: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
        color: #b0b0ff;
        text-align: center;
        padding: 30px;
        margin-top: 50px;
        border-top: 1px solid rgba(102, 126, 234, 0.3);
    }
 
    .footer-text {
        font-size: 0.9em;
        margin: 5px 0;
    }
 
    /* Price Highlight */
    .price-highlight {
        color: #667eea;
        font-size: 1.4em;
        font-weight: 800;
    }
 
    /* Rating Stars */
    .rating-stars {
        color: #ffc107;
        font-size: 1.1em;
        margin: 5px 0;
    }
 
    /* Image Preview */
    .image-preview {
        border-radius: 15px;
        box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
        margin: 15px 0;
        overflow: hidden;
    }
 
    /* Chat Container */
    [data-testid="stChatMessageContainer"] {
        padding: 20px;
    }
 
    /* Main container */
    .main-content {
        max-width: 900px;
        margin: 0 auto;
        padding: 20px;
    }
</style>
""", unsafe_allow_html=True)
 
# ---------------------------------------------------------------------------
# Page Config
# ---------------------------------------------------------------------------
st.set_page_config(
    page_title="🛒 AI Shopping Assistant",
    page_icon="🛒",
    layout="wide",
    initial_sidebar_state="expanded"
)
 
# ---------------------------------------------------------------------------
# Header
# ---------------------------------------------------------------------------
st.markdown("""
<div class="header-container">
    <div class="header-title">🛒 AI Shopping Assistant</div>
    <div class="header-caption">
        ✨ Tell me what you want — I'll search, rate, and find the perfect match for you
    </div>
</div>
""", unsafe_allow_html=True)
 
# ---------------------------------------------------------------------------
# Sidebar — Shop by Image
# ---------------------------------------------------------------------------
with st.sidebar:
    st.markdown('<div class="sidebar-header">📸 Shop by Image</div>', unsafe_allow_html=True)
    st.markdown(
        '<div class="sidebar-caption">Upload a photo and I\'ll find similar items instantly</div>',
        unsafe_allow_html=True
    )
 
    st.markdown('<div class="upload-card">', unsafe_allow_html=True)
 
    uploaded_file = st.file_uploader(
        label="Upload product image",
        type=["jpg", "jpeg", "png", "webp"],
        label_visibility="collapsed"
    )
 
    if uploaded_file:
        st.markdown('<div class="image-preview">', unsafe_allow_html=True)
        st.image(uploaded_file, use_container_width=True)
        st.markdown('</div>', unsafe_allow_html=True)
 
    if uploaded_file and st.button(
        "🔍 Find Similar Products",
        use_container_width=True,
        key="image_search_btn"
    ):
        suffix = os.path.splitext(uploaded_file.name)[1] or ".jpg"
        with tempfile.NamedTemporaryFile(delete=False, suffix=suffix) as tmp:
            tmp.write(uploaded_file.getvalue())
            image_path = tmp.name
 
        prompt = f"I uploaded a product image. Please analyze it and find similar products in the store. Image path: {image_path}"
        st.session_state.messages.append({"role": "user", "content": prompt})
        st.session_state.pending_image = uploaded_file.name
        st.rerun()
 
    st.markdown('</div>', unsafe_allow_html=True)
 
    # Sidebar decorative element
    st.markdown("---")
    st.markdown("""
    <div style='text-align: center; color: #b0b0ff; font-size: 0.85em; margin-top: 30px;'>
        💡 <strong>Pro Tips:</strong><br>
        • Be specific with your needs<br>
        • Mention budget constraints<br>
        • Ask for ratings and reviews
    </div>
    """, unsafe_allow_html=True)
 
# ---------------------------------------------------------------------------
# Chat State
# ---------------------------------------------------------------------------
if "messages" not in st.session_state:
    st.session_state.messages = []
 
# ---------------------------------------------------------------------------
# Display Chat History
# ---------------------------------------------------------------------------
st.markdown('<div class="main-content">', unsafe_allow_html=True)
 
for msg in st.session_state.messages:
    if msg["role"] == "user":
        with st.chat_message("user"):
            if msg["content"].startswith("I uploaded a product image"):
                filename = msg["content"].split("Image path:")[-1].strip()
                st.markdown(f"""
                <div class="user-message">
                    📸 Searching by image: <strong>{os.path.basename(filename)}</strong>
                </div>
                """, unsafe_allow_html=True)
            else:
                st.markdown(f"""
                <div class="user-message">
                    {msg["content"].replace("$", r"\$")}
                </div>
                """, unsafe_allow_html=True)
    else:
        with st.chat_message("assistant"):
            st.markdown(f"""
            <div class="assistant-message">
                {msg["content"].replace("$", r"\$")}
            </div>
            """, unsafe_allow_html=True)
 
# ---------------------------------------------------------------------------
# Process Image Upload (Agent Invocation)
# ---------------------------------------------------------------------------
if (
    st.session_state.messages
    and st.session_state.messages[-1]["role"] == "user"
    and "pending_image" in st.session_state
):
    with st.chat_message("assistant"):
        col1, col2, col3 = st.columns([1, 2, 1])
        with col2:
            st.markdown("""
            <div class="spinner-container">
                <div class="spinner"></div>
            </div>
            <p style='text-align: center; color: #667eea; font-weight: 600;'>
                🔍 Analyzing image and searching...
            </p>
            """, unsafe_allow_html=True)
 
        result = agent.invoke({"messages": st.session_state.messages})
        response = result["messages"][-1].content.replace("", "")
 
        st.markdown(f"""
        <div class="assistant-message">
            {response.replace("$", r"\$")}
        </div>
        """, unsafe_allow_html=True)
 
    st.session_state.messages.append({"role": "assistant", "content": response})
    del st.session_state.pending_image
    st.rerun()
 
# ---------------------------------------------------------------------------
# Chat Input
# ---------------------------------------------------------------------------
if prompt := st.chat_input(
    "💭 e.g., I want organic honey under $15 with 4+ rating...",
    key="chat_input"
):
    st.session_state.messages.append({"role": "user", "content": prompt})
    
    with st.chat_message("user"):
        st.markdown(f"""
        <div class="user-message">
            {prompt}
        </div>
        """, unsafe_allow_html=True)
 
    with st.chat_message("assistant"):
        col1, col2, col3 = st.columns([1, 2, 1])
        with col2:
            st.markdown("""
            <div class="spinner-container">
                <div class="spinner"></div>
            </div>
            <p style='text-align: center; color: #667eea; font-weight: 600;'>
                🤔 Thinking...
            </p>
            """, unsafe_allow_html=True)
 
        result = agent.invoke({"messages": st.session_state.messages})
        response = result["messages"][-1].content.replace("", "")
 
        st.markdown(f"""
        <div class="assistant-message">
            {response.replace("$", r"\$")}
        </div>
        """, unsafe_allow_html=True)
 
    st.session_state.messages.append({"role": "assistant", "content": response})
    st.rerun()
 
# ---------------------------------------------------------------------------
# Footer
# ---------------------------------------------------------------------------
st.markdown("</div>", unsafe_allow_html=True)
st.markdown("""
<div class="footer">
    <div class="footer-text">
        <strong>🛒 AI Shopping Assistant</strong> | Made with ❤️ for better shopping
    </div>
    <div class="footer-text" style='margin-top: 15px; font-size: 0.8em;'>
        ✅ Secure • 🔒 Private • ⚡ Fast
    </div>
</div>
""", unsafe_allow_html=True)