const express = require('express');
const cors = require('cors');
const axios = require('axios');

const app = express();
app.use(cors());
app.use(express.json());

const PI_API_KEY = process.env.PI_API_KEY || '';

app.get('/api/health', (req, res) => {
    res.json({ status: 'ok', message: 'Backend Render opérationnel avec Pi Network' });
});

app.post('/api/approve', async (req, res) => {
    const { paymentId } = req.body;
    try {
        await axios.post(`https://api.minepi.com/v2/payments/${paymentId}/approve`, {}, {
            headers: { Authorization: `Key ${PI_API_KEY}` }
        });
        res.json({ success: true });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});

app.post('/api/complete', async (req, res) => {
    const { paymentId, txid } = req.body;
    try {
        await axios.post(`https://api.minepi.com/v2/payments/${paymentId}/complete`, { txid }, {
            headers: { Authorization: `Key ${PI_API_KEY}` }
        });
        res.json({ success: true });
    } catch (err) {
        res.status(500).json({ error: err.message });
    }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log(`Serveur actif sur le port ${PORT}`));

