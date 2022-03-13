import * as CryptoJS from 'crypto-js';

export class Block {
  public id: number;
  public hash: string;
  public previousHash: string;
  public data: string;
  public timeStamp: number;

  constructor(id: number, hash: string, previousHash: string, data: string, timeStamp: number) {
    this.id = id;
    this.hash = hash;
    this.previousHash = previousHash;
    this.data = data;
    this.timeStamp = timeStamp;
  }

  // CryptoJS.SHA256 - функция для подсчета hesh
  static calculateBlockHash(id: number, previousHash: string, data: string, timestamp: number): string {
    return CryptoJS.SHA256(id + previousHash + data + timestamp).toString();
  }
    
  static validateStructure(block: Block): boolean {
    return  typeof block.id === 'number' && 
            typeof block.hash === 'string' && 
            typeof block.previousHash === 'string' && 
            typeof block.data === 'string' && 
            typeof block.timeStamp === 'number';
  }
}

const genesisBlock: Block = new Block(0, '23fdaf231cd!', '', 'Hello', 1);
let blockChain: [Block] = [genesisBlock];

const getBlockChain = (): Block[] => blockChain;

const getLastBlock = (): Block => blockChain[blockChain.length - 1];

const getTimeStamp = (): number => Math.round(new Date().getTime() / 1000);

function createNewBlock(data: string): Block {
  const lastBlock: Block = getLastBlock();
  const newId: number = lastBlock.id + 1;
  const newTimeStamp: number = getTimeStamp();
  const newHash: string = Block.calculateBlockHash(newId, lastBlock.hash, data, newTimeStamp);

  const newBlock: Block = new Block(newId, newHash, lastBlock.hash,  data, newTimeStamp);

  addNewBlock(newBlock);

  return newBlock;
}

function getHashForBlock(block: Block): string {
  return Block.calculateBlockHash(block.id, block.previousHash, block.data, block.timeStamp);
} 

function isBlockValid(candidateBlock: Block, lastBlock: Block): boolean {
  if (!Block.validateStructure(candidateBlock)) {
    return false;
  } else if (lastBlock.id + 1 !== candidateBlock.id) {
    return false;
  } else if (lastBlock.hash !== candidateBlock.previousHash) {
    return false;
  } else if (getHashForBlock(candidateBlock) !== candidateBlock.hash) {
    return false;
  } 
  return true;
};

function addNewBlock(candidateBlock: Block): void {
  if (isBlockValid(candidateBlock, getLastBlock())) {
    blockChain.push(candidateBlock);
  }
}


createNewBlock(`Первый блок`);
createNewBlock(`Второй блок`);
createNewBlock(`Третий блок`);
createNewBlock(`Четвертый блок`);
createNewBlock(`Пятый блок`);


console.log(blockChain);
