# 365-FINANCE
import React, { useState } from 'react';
import { View, Text, TouchableOpacity, TextInput, StyleSheet, ScrollView } from 'react-native';
import { Ionicons, MaterialIcons, FontAwesome5 } from '@expo/vector-icons';

export default function App() {
  const [currentScreen, setCurrentScreen] = useState('home');
  const [recipient, setRecipient] = useState('');
  const [amount, setAmount] = useState('');
  const [swapFrom, setSwapFrom] = useState('');
  const [swapTo, setSwapTo] = useState('');
  const [swapAmount, setSwapAmount] = useState('');

  const balances = [
    { symbol: 'USD', amount: 10000 },
    { symbol: 'EUR', amount: 10000 },
    { symbol: 'NGN', amount: 10000 },
  ];

  const renderHome = () => (
    <View style={styles.container}>
      <Text style={styles.title}>365 Finance</Text>

      <View style={styles.balanceCard}>
        <Text style={styles.balanceTitle}>Wallet Balance</Text>
        <Text style={styles.balanceAmount}>$30,000</Text>
      </View>

      <View style={styles.buttonRow}>
        <TouchableOpacity style={styles.actionButton} onPress={() => setCurrentScreen('send')}>
          <MaterialIcons name="send" size={24} color="white" />
          <Text style={styles.buttonText}>Send</Text>
        </TouchableOpacity>

        <TouchableOpacity style={styles.actionButton} onPress={() => setCurrentScreen('receive')}>
          <Ionicons name="qr-code-outline" size={24} color="white" />
          <Text style={styles.buttonText}>Receive</Text>
        </TouchableOpacity>

        <TouchableOpacity style={styles.actionButton} onPress={() => setCurrentScreen('swap')}>
          <FontAwesome5 name="exchange-alt" size={24} color="white" />
          <Text style={styles.buttonText}>Swap</Text>
        </TouchableOpacity>
      </View>

      <Text style={styles.sectionTitle}>Tokens</Text>

      <ScrollView style={styles.tokenList}>
        {balances.map((token, index) => (
          <View key={index} style={styles.tokenItem}>
            <Text style={styles.tokenSymbol}>{token.symbol}</Text>
            <Text style={styles.tokenAmount}>{token.amount}</Text>
          </View>
        ))}
      </ScrollView>
    </View>
  );

  const renderSend = () => (
    <View style={styles.container}>
      <Text style={styles.title}>Send Tokens</Text>

      <TextInput
        style={styles.input}
        placeholder="Recipient Address"
        placeholderTextColor="#999"
        value={recipient}
        onChangeText={setRecipient}
      />

      <TextInput
        style={styles.input}
        placeholder="Amount"
        placeholderTextColor="#999"
        value={amount}
        onChangeText={setAmount}
        keyboardType="numeric"
      />

      <TouchableOpacity style={styles.submitButton}>
        <Text style={styles.submitButtonText}>Send Now</Text>
      </TouchableOpacity>

      <TouchableOpacity onPress={() => setCurrentScreen('home')} style={styles.backButton}>
        <Text style={styles.backText}>Back</Text>
      </TouchableOpacity>
    </View>
  );

  const renderReceive = () => (
    <View style={styles.container}>
      <Text style={styles.title}>Receive Tokens</Text>

      <View style={styles.qrBox}>
        <Ionicons name="qr-code-outline" size={120} color="#FFD700" />
        <Text style={styles.qrText}>Your Wallet Address</Text>
        <Text style={styles.walletAddress}>F4keWa11etAddre55xxxx</Text>
      </View>

      <TouchableOpacity onPress={() => setCurrentScreen('home')} style={styles.backButton}>
        <Text style={styles.backText}>Back</Text>
      </TouchableOpacity>
    </View>
  );

  const renderSwap = () => (
    <View style={styles.container}>
      <Text style={styles.title}>Swap Tokens</Text>

      <TextInput
        style={styles.input}
        placeholder="From Token (e.g., USD)"
        placeholderTextColor="#999"
        value={swapFrom}
        onChangeText={setSwapFrom}
      />

      <TextInput
        style={styles.input}
        placeholder="To Token (e.g., EUR)"
        placeholderTextColor="#999"
        value={swapTo}
        onChangeText={setSwapTo}
      />

      <TextInput
        style={styles.input}
        placeholder="Amount"
        placeholderTextColor="#999"
        value={swapAmount}
        onChangeText={setSwapAmount}
        keyboardType="numeric"
      />

      <TouchableOpacity style={styles.submitButton}>
        <Text style={styles.submitButtonText}>Swap Now</Text>
      </TouchableOpacity>

      <TouchableOpacity onPress={() => setCurrentScreen('home')} style={styles.backButton}>
        <Text style={styles.backText}>Back</Text>
      </TouchableOpacity>
    </View>
  );

  if (currentScreen === 'send') return renderSend();
  if (currentScreen === 'receive') return renderReceive();
  if (currentScreen === 'swap') return renderSwap();
  return renderHome();
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000000',
    paddingTop: 60,
    paddingHorizontal: 20,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#FFD700', 
    marginBottom: 20,
    alignSelf: 'center',
  },
  balanceCard: {
    backgroundColor: '#1a1a1a',
    borderRadius: 16,
    padding: 20,
    alignItems: 'center',
    marginBottom: 30,
  },
  balanceTitle: {
    color: 'white',
    fontSize: 16,
    marginBottom: 10,
  },
  balanceAmount: {
    color: '#FFD700',
    fontSize: 32,
    fontWeight: 'bold',
  },
  buttonRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 30,
  },
  actionButton: {
    backgroundColor: '#FFD700',
    width: 100,
    height: 100,
    borderRadius: 16,
    justifyContent: 'center',
    alignItems: 'center',
  },
  buttonText: {
    color: 'black',
    marginTop: 5,
    fontWeight: 'bold',
  },
  sectionTitle: {
    color: '#FFD700',
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  tokenList: {
    marginBottom: 20,
  },
  tokenItem: {
    backgroundColor: '#1a1a1a',
    padding: 15,
    borderRadius: 12,
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 10,
  },
  tokenSymbol: {
    color: 'white',
    fontSize: 18,
  },
  tokenAmount: {
    color: '#FFD700',
    fontSize: 18,
    fontWeight: 'bold',
  },
  input: {
    backgroundColor: '#1a1a1a',
    color: 'white',
    padding: 15,
    borderRadius: 12,
    marginBottom: 15,
  },
  submitButton: {
    backgroundColor: '#FFD700',
    padding: 15,
    borderRadius: 12,
    alignItems: 'center',
    marginBottom: 20,
  },
  submitButtonText: {
    fontWeight: 'bold',
    color: 'black',
  },
  backButton: {
    padding: 10,
    backgroundColor: '#FFD700',
    borderRadius: 8,
    alignSelf: 'center',
  },
  backText: {
    color: 'black',
    fontWeight: 'bold',
  },
  qrBox: {
    backgroundColor: '#1a1a1a',
    padding: 30,
    borderRadius: 16,
    alignItems: 'center',
    marginBottom: 20,
  },
  qrText: {
    color: '#FFD700',
    marginTop: 10,
    fontSize: 16,
  },
  walletAddress: {
    color: 'white',
    marginTop: 5,
    fontSize: 14,
  },
});
